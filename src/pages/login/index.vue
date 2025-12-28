<template>
  <view class="login-page">
    <!-- 顶部装饰 -->
    <view class="header">
      <view class="header-bg" />
    </view>

    <!-- Logo区域 -->
    <view class="logo-section">
      <image class="logo" src="/static/logo.png" mode="aspectFit" />
      <text class="title">CRM外呼助手</text>
    </view>

    <!-- 登录表单 -->
    <view class="form-section">
      <view class="input-group">
        <view class="input-item">
          <text class="icon">👤</text>
          <input
            v-model="username"
            placeholder="请输入用户名"
            placeholder-class="placeholder"
            :disabled="isLoading"
          />
        </view>

        <view class="input-item">
          <text class="icon">🔒</text>
          <input
            v-model="password"
            type="password"
            placeholder="请输入密码"
            placeholder-class="placeholder"
            :disabled="isLoading"
            @confirm="handleLogin"
          />
        </view>
      </view>

      <view class="options">
        <view class="checkbox-item" @tap="rememberPassword = !rememberPassword">
          <view class="checkbox" :class="{ checked: rememberPassword }">
            <text v-if="rememberPassword">✓</text>
          </view>
          <text>记住密码</text>
        </view>
      </view>

      <button
        class="btn-login"
        @tap="handleLogin"
        :loading="isLoading"
        :disabled="!canLogin"
      >
        登 录
      </button>
    </view>

    <!-- 底部服务器信息 -->
    <view class="server-info">
      <text class="server-label">服务器: </text>
      <text class="server-url">{{ serverStore.displayUrl }}</text>
      <text class="server-switch" @tap="goToServerConfig">切换</text>
    </view>
  </view>
</template>

<script setup lang="ts">
import { ref, computed, onMounted } from 'vue'
import { useServerStore } from '@/stores/server'
import { useUserStore } from '@/stores/user'
import { login } from '@/api/auth'

const serverStore = useServerStore()
const userStore = useUserStore()

const username = ref('')
const password = ref('')
const rememberPassword = ref(true)
const isLoading = ref(false)

const canLogin = computed(() => {
  return username.value.trim() && password.value.trim() && !isLoading.value
})

onMounted(() => {
  // 恢复记住的用户名和密码
  const savedUsername = uni.getStorageSync('savedUsername')
  const savedPassword = uni.getStorageSync('savedPassword')
  if (savedUsername) {
    username.value = savedUsername
  }
  if (savedPassword) {
    password.value = savedPassword
  }
})

// 登录
const handleLogin = async () => {
  if (!canLogin.value) return

  isLoading.value = true

  try {
    // 获取设备信息
    const systemInfo = uni.getSystemInfoSync()

    const result = await login({
      username: username.value,
      password: password.value,
      deviceInfo: {
        deviceId: systemInfo.deviceId || '',
        deviceName: systemInfo.deviceModel || '未知设备',
        deviceModel: systemInfo.deviceModel || '',
        osType: systemInfo.platform === 'ios' ? 'ios' : 'android',
        osVersion: systemInfo.system || '',
        appVersion: '1.0.0'
      }
    })

    // 保存登录信息
    userStore.setLoginInfo(result)

    // 确保token已保存
    console.log('登录成功，token已保存:', userStore.token ? '有' : '无')

    // 记住密码
    if (rememberPassword.value) {
      uni.setStorageSync('savedUsername', username.value)
      uni.setStorageSync('savedPassword', password.value)
    } else {
      uni.removeStorageSync('savedUsername')
      uni.removeStorageSync('savedPassword')
    }

    uni.showToast({ title: '登录成功', icon: 'success' })

    // 跳转到首页（延迟确保状态同步）
    setTimeout(() => {
      console.log('跳转首页，当前token:', userStore.token ? '有' : '无')
      uni.switchTab({ url: '/pages/index/index' })
    }, 1200)
  } catch (e: any) {
    uni.showToast({
      title: e.message || '登录失败',
      icon: 'none'
    })
  } finally {
    isLoading.value = false
  }
}

// 切换服务器
const goToServerConfig = () => {
  uni.navigateTo({ url: '/pages/server-config/index' })
}
</script>

<style lang="scss" scoped>
.login-page {
  min-height: 100vh;
  background: #f5f5f5;
  display: flex;
  flex-direction: column;

  .header {
    height: 300rpx;
    position: relative;

    .header-bg {
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
      height: 400rpx;
      background: linear-gradient(135deg, #6EE7B7 0%, #34D399 100%);
      border-radius: 0 0 60rpx 60rpx;
    }
  }

  .logo-section {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-top: -100rpx;
    position: relative;
    z-index: 1;

    .logo {
      width: 140rpx;
      height: 140rpx;
      background: #fff;
      border-radius: 32rpx;
      padding: 20rpx;
      box-shadow: 0 8rpx 32rpx rgba(0, 0, 0, 0.1);
    }

    .title {
      font-size: 40rpx;
      font-weight: bold;
      color: #1F2937;
      margin-top: 24rpx;
    }
  }

  .form-section {
    padding: 60rpx 48rpx;

    .input-group {
      background: #fff;
      border-radius: 24rpx;
      overflow: hidden;
      box-shadow: 0 4rpx 16rpx rgba(0, 0, 0, 0.05);

      .input-item {
        display: flex;
        align-items: center;
        padding: 32rpx;
        border-bottom: 1rpx solid #F3F4F6;

        &:last-child {
          border-bottom: none;
        }

        .icon {
          font-size: 36rpx;
          margin-right: 24rpx;
        }

        input {
          flex: 1;
          font-size: 32rpx;
          color: #1F2937;
        }

        .placeholder {
          color: #9CA3AF;
        }
      }
    }

    .options {
      display: flex;
      justify-content: space-between;
      margin: 32rpx 0;

      .checkbox-item {
        display: flex;
        align-items: center;

        .checkbox {
          width: 36rpx;
          height: 36rpx;
          border: 2rpx solid #D1D5DB;
          border-radius: 8rpx;
          margin-right: 12rpx;
          display: flex;
          align-items: center;
          justify-content: center;

          &.checked {
            background: #34D399;
            border-color: #34D399;

            text {
              color: #fff;
              font-size: 24rpx;
            }
          }
        }

        text {
          font-size: 26rpx;
          color: #6B7280;
        }
      }
    }

    .btn-login {
      width: 100%;
      height: 96rpx;
      background: linear-gradient(135deg, #6EE7B7 0%, #34D399 100%);
      color: #fff;
      font-size: 34rpx;
      font-weight: 500;
      border-radius: 48rpx;
      border: none;
      margin-top: 20rpx;

      &[disabled] {
        opacity: 0.5;
      }
    }
  }

  .server-info {
    position: fixed;
    bottom: 80rpx;
    left: 0;
    right: 0;
    text-align: center;
    font-size: 24rpx;

    .server-label {
      color: #9CA3AF;
    }

    .server-url {
      color: #6B7280;
    }

    .server-switch {
      color: #34D399;
      margin-left: 16rpx;
      text-decoration: underline;
    }
  }
}
</style>
