<template>
  <view class="agreement-page">
    <view class="content">
      <text class="title">用户服务协议</text>
      <text class="update-time">更新日期：2026年1月2日</text>

      <view class="section">
        <text class="section-title">一、协议的接受与修改</text>
        <text class="section-content">
          欢迎使用CRM外呼助手（以下简称"本应用"）。本应用由运营方（以下简称"我们"）提供。在您使用本应用之前，请您仔细阅读本《用户服务协议》（以下简称"本协议"）。

          当您点击"同意"或以其他方式确认接受本协议，或您下载、安装、使用本应用时，即表示您已充分阅读、理解并同意接受本协议的全部内容。如您不同意本协议的任何条款，请勿使用本应用。

          我们有权根据业务发展需要，对本协议进行修改。修改后的协议将在本应用内公布，您继续使用本应用即视为您接受修改后的协议。
        </text>
      </view>

      <view class="section">
        <text class="section-title">二、服务内容</text>
        <text class="section-content">
          本应用是一款企业级客户关系管理（CRM）移动办公工具，主要提供以下服务：

          1. 外呼管理：支持通过工作手机发起外呼，记录通话信息，管理通话录音；
          2. 客户管理：查看和管理客户信息，记录客户跟进情况；
          3. 订单管理：查看订单状态，处理订单相关事务；
          4. 数据统计：查看个人业绩数据和通话统计；
          5. 消息通知：接收系统消息和业务提醒；
          6. 其他企业办公相关功能。

          本应用仅供企业内部员工使用，需要通过企业管理员分配的账号登录使用。
        </text>
      </view>

      <view class="section">
        <text class="section-title">三、用户账号</text>
        <text class="section-content">
          1. 账号获取：您的账号由企业管理员创建和分配，您应妥善保管账号和密码；
          2. 账号安全：您应对账号下的所有行为负责，如发现账号被盗用或存在安全风险，应立即通知企业管理员；
          3. 账号使用：您不得将账号转让、出借给他人使用，不得使用他人账号；
          4. 账号注销：当您离职或不再需要使用本应用时，企业管理员将注销您的账号。
        </text>
      </view>

      <view class="section">
        <text class="section-title">四、用户行为规范</text>
        <text class="section-content">
          您在使用本应用时，应遵守以下规范：

          1. 遵守国家法律法规，不得利用本应用从事违法违规活动；
          2. 遵守企业规章制度，按照企业要求使用本应用；
          3. 不得骚扰、欺诈客户，不得泄露客户隐私信息；
          4. 不得恶意拨打骚扰电话，不得进行电话诈骗等违法行为；
          5. 不得破坏、干扰本应用的正常运行；
          6. 不得利用本应用传播违法、有害信息；
          7. 不得进行任何可能损害我们或第三方合法权益的行为。

          如您违反上述规范，我们有权暂停或终止您使用本应用的权利，并保留追究法律责任的权利。
        </text>
      </view>

      <view class="section">
        <text class="section-title">五、知识产权</text>
        <text class="section-content">
          1. 本应用的所有内容，包括但不限于文字、图片、音频、视频、软件、程序、界面设计、版面框架等，均受知识产权法律法规保护；
          2. 未经我们书面许可，您不得复制、修改、传播、出售本应用的任何内容；
          3. 您在使用本应用过程中产生的业务数据，其所有权归属于您所在企业。
        </text>
      </view>

      <view class="section">
        <text class="section-title">六、免责声明</text>
        <text class="section-content">
          1. 因网络状况、通讯线路等原因造成的服务中断或延迟，我们不承担责任；
          2. 因不可抗力（如自然灾害、政府行为等）导致的服务中断，我们不承担责任；
          3. 因您自身原因（如账号泄露、操作失误等）造成的损失，我们不承担责任；
          4. 本应用可能包含第三方服务链接，我们对第三方服务的内容和行为不承担责任；
          5. 您使用本应用进行的通话内容和业务行为，由您自行负责。
        </text>
      </view>

      <view class="section">
        <text class="section-title">七、协议终止</text>
        <text class="section-content">
          1. 您可以随时停止使用本应用；
          2. 如您违反本协议，我们有权终止向您提供服务；
          3. 协议终止后，您应停止使用本应用，我们有权删除您的账号和相关数据。
        </text>
      </view>

      <view class="section">
        <text class="section-title">八、其他条款</text>
        <text class="section-content">
          1. 本协议的订立、执行和解释均适用中华人民共和国法律；
          2. 因本协议引起的争议，双方应友好协商解决；协商不成的，任何一方均可向我们所在地人民法院提起诉讼；
          3. 本协议的任何条款被认定为无效或不可执行，不影响其他条款的效力；
          4. 本协议构成您与我们之间关于使用本应用的完整协议。

          如您对本协议有任何疑问，请联系企业管理员或通过应用内反馈功能与我们联系。
        </text>
      </view>
    </view>
  </view>
</template>

<script setup lang="ts">
</script>

<style lang="scss" scoped>
.agreement-page {
  min-height: 100vh;
  background: #fff;

  .content {
    padding: 32rpx;

    .title {
      display: block;
      font-size: 40rpx;
      font-weight: bold;
      color: #1F2937;
      text-align: center;
      margin-bottom: 16rpx;
    }

    .update-time {
      display: block;
      font-size: 24rpx;
      color: #9CA3AF;
      text-align: center;
      margin-bottom: 40rpx;
    }

    .section {
      margin-bottom: 40rpx;

      .section-title {
        display: block;
        font-size: 32rpx;
        font-weight: bold;
        color: #1F2937;
        margin-bottom: 16rpx;
      }

      .section-content {
        display: block;
        font-size: 28rpx;
        color: #4B5563;
        line-height: 1.8;
        text-align: justify;
      }
    }
  }
}
</style>
