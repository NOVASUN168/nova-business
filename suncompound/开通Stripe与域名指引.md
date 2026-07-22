# 开通 Stripe + 申请正式网址 · 中文指引（Nova / 悉尼公司）

> 你的临时上线网址（今天就能用）：
> **https://7a66d33d6cec4c2bb168688992179b78.app.codebuddy.work**
>
> 落地页源码：`suncompound-site/index.html`（可随时让我改文案/配色）

---

## 一、先搞清楚的 3 件事

1. **你在悉尼、有公司 → Stripe 澳大利亚完全支持**，不需要香港/美国主体。
2. **Stripe 要填一个"网站 URL"**——你刚才拿到的临时网址就能填；等正式域名 `suncompound.com` 注册好，再换上去。
3. **注册域名要你本人付款 + 填个人信息**，我不能直接代付。下面每一步的英文界面我都翻译好了，你照着点就行。

---

## 二、注册域名 suncompound.com（推荐注册商：Porkbun，便宜、界面干净）

> Porkbun 官网：https://porkbun.com
> 支持国际信用卡 / PayPal，.com 大概 $10/年（约 ¥70）。

### 第 1 步：搜索并加入购物车
- 打开 https://porkbun.com → 顶部搜索框输入 `suncompound.com` → 按回车。
- 页面显示 `suncompound.com` 一行，右侧如果是 **Add to Cart**（加入购物车）说明可注册 ✅。
- 点 **Add to Cart**。

### 第 2 步：结账（Checkout）
- 点右上角购物车图标 → **Checkout**（结账）。
- 如果提示 **Create Account / Sign In**（创建账户/登录）：
  - 点 **Create Account**，填邮箱 + 设置密码。
  - 验证邮箱里的确认信（去收件箱点链接）。
- 回到购物车点 **Checkout**。

### 第 3 步：填注册信息（WHOIS 联系人）
- **Registry Information / Contact Information**（注册联系人）：
  - First Name（名）：填你的名
  - Last Name（姓）：Sun（或你的姓）
  - Organization（公司，可留空或填公司名）
  - Email / Phone / Address：填悉尼的真实地址和电话（Stripe 和域名商都要真实信息）
- **WHOIS Privacy**（隐私保护）：默认会勾选 **Free Privacy**（免费隐私，强烈建议开启，别人查不到你的电话地址）。保持不变即可。
- **Registration Period**（注册年限）：默认 1 年，可改成 2~3 年省心。

### 第 4 步：付款
- **Payment Method**（付款方式）：选 **Credit/Debit Card** 或 **PayPal**。
- 填卡号、有效期、CVV、账单地址 → 点 **Pay / Complete Purchase**（完成购买）。
- 付款成功后，域名就归你了，进入 **Dashboard（控制台）**。

> ⚠️ 付款前再确认一次：域名是秒级变动的，下单时若提示已被注册，换 `suncompound.com.au`（也已查过可注册，但需要你有匹配的公司名/Business Name）。

---

## 三、把正式域名指向你的网站（DNS 解析）

你的网站现在托管在 CloudStudio。要让 `suncompound.com` 打开就是你的落地页，有两种做法：

### 方案 A（最快，先能用）：用临时网址，暂不绑域名
Stripe 申请阶段直接填临时网址即可，域名注册好后再处理绑定。

### 方案 B（正式，自定义域名）：重新部署到支持自定义域名的平台
CloudStudio 的分享链接不方便绑自有域名。建议把同一个 `index.html` 部署到 **Netlify**（免费、支持自定义域名、对中文用户也友好）：
1. 打开 https://app.netlify.com → 注册/登录（可用 GitHub 登录）。
2. 进 **Sites** → **Add new site** → **Deploy manually**（手动部署）→ 把 `index.html` 拖进去。
3. 部署完会给一个 `xxx.netlify.app` 网址（也能直接用于 Stripe）。
4. 在 Site settings → **Domain management** → **Add custom domain** 输入 `suncompound.com`。
5. 回 Porkbun → 该域名 **DNS** → 添加 **Netlify 给你的 DNS 记录**（通常是两条 A 记录或一条 CNAME，Netlify 页面会写明复制哪几条）。
6. 等 10 分钟~几小时生效，浏览器打开 `suncompound.com` 就是你的网站。

> 这步如果卡住，随时叫我，我一步步带你点。

---

## 四、正式开通 Stripe（澳大利亚）

> 地址用澳大利亚版：https://dashboard.stripe.com/register （地区选 Australia）

1. **邮箱注册** → 验证邮箱。
2. **国家/地区**：选 **Australia**。
3. **业务类型（Business type）**：选 **Company**（公司）→ 填：
   - 公司法定名称、ABN（澳大利亚商业号码）、ACN（如有）
   - 公司地址（悉尼）
   - 业务描述：写 *"Paid subscription community & educational content about investing and personal growth"*（投资认知与成长类付费订阅内容）
4. **网站 URL**：先填临时网址，域名好了换成 `https://suncompound.com`。
5. **银行账户（Payouts）**：填你的澳大利亚公司对公/绑定银行账户，Stripe 收款后会打款到这里。
6. **身份验证**：上传你的证件（护照/驾照）+ 可能要公司文件。Stripe 审核一般几分钟到 1~2 天。
7. 激活后，在 Dashboard 左侧 **Payment Links** → **New**（新建）→ 设置金额 $19/月、商品名"内容星球会员" → 生成一条 `https://buy.stripe.com/xxxx` 链接。

### 把付款链接接到落地页
- 打开 `suncompound-site/index.html`，找到这一行：
  ```html
  <a class="stripe-btn" href="https://buy.stripe.com/REPLACE_WITH_YOUR_LINK">
  ```
- 把 `REPLACE_WITH_YOUR_LINK` 换成你刚生成的 Stripe 链接，保存。
- 告诉我"重新部署"，我帮你更新上线。

---

## 五、商标小提醒（先知道，不急）
域名到手 ≠ 商标到手。如果以后要做大、印物料，建议在 **IP Australia**（澳大利亚）和 **USPTO**（美国）查一下 "Sun Compound" 在第 35 类（广告销售）、36 类（金融）、41 类（教育）有没有冲突。现在规模小没关系，先记着。

---

## 六、给你的行动清单（按顺序）
- [ ] 去 Porkbun 注册 `suncompound.com`（照第二步点）
- [ ] 把 Stripe 地区选 Australia，先用临时网址提交申请
- [ ] Stripe 激活后生成 Payment Link，发给我，我帮你接进落地页并重新部署
- [ ] 想绑正式域名时，照第三步方案 B 操作（或叫我带你做）

有任何一步英文看不懂，截图发我，我逐句翻给你。
