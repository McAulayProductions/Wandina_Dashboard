
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Wandina Weekly Command + Trigger Dashboard</title>
  <style>
    :root {
      --bg: #0f172a;
      --panel: #111827;
      --soft: #1f2937;
      --line: #334155;
      --text: #e5e7eb;
      --muted: #94a3b8;
      --green: #14532d;
      --green2: #22c55e;
      --amber: #78350f;
      --amber2: #f59e0b;
      --red: #7f1d1d;
      --red2: #ef4444;
      --blue: #1d4ed8;
      --blue2: #60a5fa;
    }
    * { box-sizing: border-box; }
    body {
      margin: 0;
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Arial, sans-serif;
      background: linear-gradient(180deg, #020617 0%, #0f172a 100%);
      color: var(--text);
      line-height: 1.45;
    }
    .wrap {
      max-width: 1180px;
      margin: 0 auto;
      padding: 16px;
    }
    .hero {
      background: linear-gradient(135deg, rgba(29,78,216,.25), rgba(15,23,42,.8));
      border: 1px solid var(--line);
      border-radius: 18px;
      padding: 18px;
      margin-bottom: 16px;
    }
    .hero h1 { margin: 0 0 6px; font-size: 1.45rem; }
    .hero p { margin: 6px 0; color: var(--muted); }
    .grid {
      display: grid;
      grid-template-columns: repeat(12, 1fr);
      gap: 14px;
    }
    .card {
      grid-column: span 12;
      background: rgba(17,24,39,.92);
      border: 1px solid var(--line);
      border-radius: 18px;
      padding: 16px;
      box-shadow: 0 10px 30px rgba(0,0,0,.18);
    }
    @media (min-width: 900px) {
      .span-4 { grid-column: span 4; }
      .span-5 { grid-column: span 5; }
      .span-6 { grid-column: span 6; }
      .span-7 { grid-column: span 7; }
      .span-8 { grid-column: span 8; }
    }
    h2, h3 { margin: 0 0 12px; }
    h2 { font-size: 1.05rem; }
    h3 { font-size: .95rem; color: #cbd5e1; }
    .sub { color: var(--muted); font-size: .92rem; margin-top: -4px; margin-bottom: 10px; }
    .metrics {
      display: grid;
      grid-template-columns: repeat(2, minmax(0, 1fr));
      gap: 10px;
    }
    @media (min-width: 700px) {
      .metrics { grid-template-columns: repeat(4, minmax(0, 1fr)); }
    }
    .metric {
      background: var(--soft);
      border: 1px solid var(--line);
      border-radius: 14px;
      padding: 12px;
    }
    .metric .label { color: var(--muted); font-size: .78rem; }
    .metric .value { font-size: 1.25rem; font-weight: 700; margin-top: 4px; }
    .metric .small { font-size: .78rem; color: var(--muted); margin-top: 4px; }
    .pillbar { display: flex; flex-wrap: wrap; gap: 8px; margin-top: 10px; }
    .pill {
      border-radius: 999px;
      padding: 8px 12px;
      font-weight: 700;
      font-size: .82rem;
      border: 1px solid transparent;
    }
    .green { background: rgba(20,83,45,.4); color: #bbf7d0; border-color: rgba(34,197,94,.4); }
    .amber { background: rgba(120,53,15,.4); color: #fde68a; border-color: rgba(245,158,11,.4); }
    .red { background: rgba(127,29,29,.45); color: #fecaca; border-color: rgba(239,68,68,.45); }
    .blue { background: rgba(29,78,216,.35); color: #dbeafe; border-color: rgba(96,165,250,.4); }
    .fields {
      display: grid;
      grid-template-columns: repeat(2, minmax(0, 1fr));
      gap: 10px;
    }
    @media (min-width: 800px) {
      .fields-3 { grid-template-columns: repeat(3, minmax(0, 1fr)); }
      .fields-4 { grid-template-columns: repeat(4, minmax(0, 1fr)); }
    }
    label { display:block; font-size: .82rem; color: #cbd5e1; margin-bottom: 4px; }
    input, select {
      width: 100%;
      background: #0b1220;
      border: 1px solid var(--line);
      color: var(--text);
      padding: 10px 11px;
      border-radius: 12px;
      outline: none;
    }
    input:focus, select:focus { border-color: var(--blue2); }
    .row {
      display:grid;
      gap:12px;
      grid-template-columns: repeat(12, 1fr);
    }
    .row > div { grid-column: span 12; }
    @media (min-width: 700px){
      .row.two > div { grid-column: span 6; }
      .row.three > div { grid-column: span 4; }
    }
    .checklist { display:grid; gap:8px; }
    .check {
      display:flex; gap:10px; align-items:flex-start;
      background: var(--soft);
      border:1px solid var(--line);
      border-radius: 12px; padding: 10px 12px;
    }
    .check input { width: 18px; height: 18px; margin-top: 2px; }
    .check strong { display:block; }
    .check span { color: var(--muted); font-size: .86rem; }
    .note {
      margin-top: 10px;
      padding: 10px 12px;
      background: rgba(29,78,216,.12);
      border: 1px solid rgba(96,165,250,.25);
      border-radius: 12px;
      color: #dbeafe;
      font-size: .88rem;
    }
    .warn {
      margin-top: 10px;
      padding: 10px 12px;
      background: rgba(127,29,29,.18);
      border: 1px solid rgba(239,68,68,.25);
      border-radius: 12px;
      color: #fee2e2;
      font-size: .88rem;
    }
    table {
      width: 100%; border-collapse: collapse; font-size: .9rem;
      overflow: hidden; border-radius: 12px;
    }
    th, td {
      padding: 10px 8px; border-bottom: 1px solid var(--line); text-align: left;
    }
    th { color: #cbd5e1; }
    tr:last-child td { border-bottom: none; }
    .footer {
      margin: 18px 0 26px; color: var(--muted); font-size: .84rem;
    }
    .mono { font-variant-numeric: tabular-nums; }
  </style>
</head>
<body>
  <div class="wrap">
    <section class="hero">
      <h1>Wandina Weekly Command + Trigger Dashboard</h1>
      <p>Built around your actual decision rule: treat the Wandina debt as one investment position for strategy, but keep a separate tax cost base for CGT.</p>
      <div class="pillbar">
        <div class="pill blue">PPOR rate: 5.97% P&amp;I</div>
        <div class="pill blue">IP rate: 6.39% IO</div>
        <div class="pill blue">Guaranteed rent: $700/wk for 2 years</div>
      </div>
    </section>

    <div class="grid">
      <section class="card span-8">
        <h2>Core control panel</h2>
        <div class="sub">Edit these only when the facts change. Everything below updates automatically.</div>
        <div class="fields fields-4">
          <div>
            <label for="pporBalance">PPOR balance</label>
            <input id="pporBalance" type="number" step="1000" value="557000" />
          </div>
          <div>
            <label for="pporRate">PPOR rate %</label>
            <input id="pporRate" type="number" step="0.01" value="5.97" />
          </div>
          <div>
            <label for="pporRepay">PPOR weekly repayment</label>
            <input id="pporRepay" type="number" step="1" value="763" />
          </div>
          <div>
            <label for="pporYears">PPOR years remaining</label>
            <input id="pporYears" type="number" step="0.1" value="28.5" />
          </div>
          <div>
            <label for="offsetNow">Current offset</label>
            <input id="offsetNow" type="number" step="100" value="35000" />
          </div>
          <div>
            <label for="offsetFloor">Offset floor alert</label>
            <input id="offsetFloor" type="number" step="100" value="30000" />
          </div>
          <div>
            <label for="ipDebt">Wandina total debt</label>
            <input id="ipDebt" type="number" step="1000" value="588000" />
          </div>
          <div>
            <label for="ipRate">Wandina rate %</label>
            <input id="ipRate" type="number" step="0.01" value="6.39" />
          </div>
          <div>
            <label for="rentWeekly">Guaranteed rent / week</label>
            <input id="rentWeekly" type="number" step="10" value="700" />
          </div>
          <div>
            <label for="otherCosts">Other annual IP cash costs</label>
            <input id="otherCosts" type="number" step="100" value="7500" />
          </div>
          <div>
            <label for="deprAnnual">Annual depreciation estimate</label>
            <input id="deprAnnual" type="number" step="100" value="12000" />
          </div>
          <div>
            <label for="taxRate">Marginal tax rate %</label>
            <input id="taxRate" type="number" step="0.5" value="39" />
          </div>
        </div>
      </section>

      <section class="card span-4">
        <h2>Immediate verdict</h2>
        <div class="metrics">
          <div class="metric">
            <div class="label">IP interest / week</div>
            <div class="value mono" id="mIpInterestW">$0</div>
            <div class="small">Interest-only at current rate</div>
          </div>
          <div class="metric">
            <div class="label">Pre-tax hold / week</div>
            <div class="value mono" id="mPretaxW">$0</div>
            <div class="small">Rent less interest and cash costs</div>
          </div>
          <div class="metric">
            <div class="label">After-tax hold / week</div>
            <div class="value mono" id="mAftertaxW">$0</div>
            <div class="small">Approx with depreciation</div>
          </div>
          <div class="metric">
            <div class="label">PAYG variation / week</div>
            <div class="value mono" id="mPaygW">$0</div>
            <div class="small">Approx smoothing benefit</div>
          </div>
        </div>
        <div class="pillbar" id="statusBar"></div>
      </section>

      <section class="card span-7">
        <h2>Sell decision engine</h2>
        <div class="sub">This converts Wandina into PPOR-destruction power and tests the tax damage before you sell.</div>
        <div class="fields fields-4">
          <div>
            <label for="salePrice">Target sale price</label>
            <input id="salePrice" type="number" step="1000" value="780000" />
          </div>
          <div>
            <label for="sellCostPct">Selling costs %</label>
            <input id="sellCostPct" type="number" step="0.1" value="3.0" />
          </div>
          <div>
            <label for="taxCostBase">Tax cost base</label>
            <input id="taxCostBase" type="number" step="1000" value="608000" />
          </div>
          <div>
            <label for="capWorksClaimed">Capital works already claimed</label>
            <input id="capWorksClaimed" type="number" step="100" value="0" />
          </div>
          <div>
            <label for="acqDate">Acquisition contract date</label>
            <input id="acqDate" type="date" value="2025-10-25" />
          </div>
          <div>
            <label for="saleContractDate">Planned sale contract date</label>
            <input id="saleContractDate" type="date" value="2026-11-01" />
          </div>
          <div>
            <label for="offsetInjectionPct">Sale cash to offset %</label>
            <input id="offsetInjectionPct" type="number" step="1" value="100" />
          </div>
          <div>
            <label for="guaranteeEnds">Guaranteed rent ends</label>
            <input id="guaranteeEnds" type="date" value="2028-06-30" />
          </div>
        </div>
        <div class="metrics" style="margin-top:12px;">
          <div class="metric">
            <div class="label">12-month CGT status</div>
            <div class="value mono" id="mDiscountStatus">—</div>
            <div class="small" id="mDiscountDays">—</div>
          </div>
          <div class="metric">
            <div class="label">Approx CGT</div>
            <div class="value mono" id="mCgt">$0</div>
            <div class="small">Uses cost base minus capital works claimed</div>
          </div>
          <div class="metric">
            <div class="label">Net cash after debt + tax</div>
            <div class="value mono" id="mNetCash">$0</div>
            <div class="small">Available before any split allocation</div>
          </div>
          <div class="metric">
            <div class="label">Interest saved / year</div>
            <div class="value mono" id="mInterestSaved">$0</div>
            <div class="small">If sale cash goes to offset</div>
          </div>
        </div>
        <div class="note" id="saleAdvice"></div>
        <div class="warn">For strategy, using one debt number is fine. For CGT, debt is <strong>not</strong> the tax cost base. The tax cost base is your land/build/acquisition cost plus eligible costs, reduced by capital works already claimed. Div 40 items can also trigger a balancing adjustment on sale.</div>
      </section>

      <section class="card span-5">
        <h2>PPOR acceleration</h2>
        <div class="sub">Same repayment, different speed. This estimates what sale proceeds do to your timeline.</div>
        <div class="metrics">
          <div class="metric">
            <div class="label">Current payoff horizon</div>
            <div class="value mono" id="mBaseYears">0.0y</div>
            <div class="small">Approx from today</div>
          </div>
          <div class="metric">
            <div class="label">With sale cash in offset</div>
            <div class="value mono" id="mNewYears">0.0y</div>
            <div class="small">Approx from today</div>
          </div>
          <div class="metric">
            <div class="label">Years cut</div>
            <div class="value mono" id="mYearsCut">0.0y</div>
            <div class="small">Speed gained</div>
          </div>
          <div class="metric">
            <div class="label">Offset after sale</div>
            <div class="value mono" id="mOffsetAfter">$0</div>
            <div class="small">Before any redraw or splits</div>
          </div>
        </div>
        <div class="note" id="pporAdvice"></div>
      </section>

      <section class="card span-6">
        <h2>Weekly command system</h2>
        <div class="sub">Run this every Friday. No guessing. No drifting.</div>
        <div class="checklist">
          <label class="check"><input type="checkbox" /><div><strong>Offset check</strong><span>Log current offset. If below the floor, freeze avoidable spend and review the next 14 days.</span></div></label>
          <label class="check"><input type="checkbox" /><div><strong>Builder progress check</strong><span>Record exact stage, next trade booked, and whether any material or labour delays were raised.</span></div></label>
          <label class="check"><input type="checkbox" /><div><strong>Market pulse</strong><span>Check Wandina and nearby comparable sales, new listings, and whether days-on-market are stretching.</span></div></label>
          <label class="check"><input type="checkbox" /><div><strong>IP cashflow check</strong><span>Compare actual rent and expenses to dashboard assumptions. Fix reality, not the model.</span></div></label>
          <label class="check"><input type="checkbox" /><div><strong>Tax smoothing check</strong><span>Confirm PAYG variation is active and the weekly benefit is actually landing in cashflow.</span></div></label>
          <label class="check"><input type="checkbox" /><div><strong>Sale readiness check</strong><span>Ask one hard question: if the right number appeared today, would I be ready to sign?</span></div></label>
        </div>
      </section>

      <section class="card span-6">
        <h2>Trigger dashboard</h2>
        <div class="sub">These are decision rules, not feelings.</div>
        <table>
          <thead>
            <tr><th>Zone</th><th>Conditions</th><th>Action</th></tr>
          </thead>
          <tbody>
            <tr>
              <td><span class="pill green">GREEN</span></td>
              <td>Value under strong-exit zone, 12-month discount not yet available, or build still incomplete.</td>
              <td>Hold. Optimise tax. Track build weekly. Preserve offset.</td>
            </tr>
            <tr>
              <td><span class="pill amber">AMBER</span></td>
              <td>Approaching target value, build nearly complete, 12-month discount date getting close.</td>
              <td>Prepare sale pack, tighten comps, pressure-test agent assumptions, do not sign too early.</td>
            </tr>
            <tr>
              <td><span class="pill red">RED</span></td>
              <td>Target price achieved, contract date qualifies for 50% discount, market momentum softening.</td>
              <td>Execute sell and route net cash to offset unless a better tax-year split is proven.</td>
            </tr>
          </tbody>
        </table>
        <div class="note" id="triggerReadout"></div>
      </section>

      <section class="card span-12">
        <h2>CGT timing rules</h2>
        <div class="row three">
          <div class="note"><strong>Rule 1:</strong> The CGT event is usually the <strong>sale contract date</strong>, not settlement. If you need the 12-month discount, the contract date must clear the threshold.</div>
          <div class="note"><strong>Rule 2:</strong> If you can choose between tax years, the lower-income year usually wins because the taxable gain is added to your other taxable income.</div>
          <div class="note"><strong>Rule 3:</strong> If you have capital losses elsewhere, line the sale up with them. They can offset capital gains before the discount method is applied.</div>
        </div>
        <div class="row two" style="margin-top:12px;">
          <div class="warn"><strong>Watch-out:</strong> capital works deductions already claimed can reduce the property’s cost base for CGT. Div 40 items included in the sale can create a balancing adjustment event rather than just a pure CGT result.</div>
          <div class="note"><strong>Practical move:</strong> ask your accountant for a pre-sale worksheet that splits: selling costs, adjusted cost base, capital works claimed, Div 40 adjustable values, and the estimated PAYG instalment or tax shortfall before you sign a contract.</div>
        </div>
      </section>
    </div>

    <div class="footer">
      Save this file and keep it beside your main finance app, or merge the logic into your existing Finance Control build. It stores values locally in your browser.
    </div>
  </div>

  <script>
    const ids = [
      'pporBalance','pporRate','pporRepay','pporYears','offsetNow','offsetFloor','ipDebt','ipRate',
      'rentWeekly','otherCosts','deprAnnual','taxRate','salePrice','sellCostPct','taxCostBase',
      'capWorksClaimed','acqDate','saleContractDate','offsetInjectionPct','guaranteeEnds'
    ];

    function $(id){ return document.getElementById(id); }
    function n(id){ return parseFloat($(id).value || 0); }
    function money(x){
      const sign = x < 0 ? '-' : '';
      const v = Math.abs(x);
      return sign + '$' + v.toLocaleString(undefined,{maximumFractionDigits:0});
    }
    function money1(x){
      const sign = x < 0 ? '-' : '';
      const v = Math.abs(x);
      return sign + '$' + v.toLocaleString(undefined,{minimumFractionDigits:0, maximumFractionDigits:0});
    }
    function yearsToPayoff(principal, annualRate, weeklyPayment, offset=0){
      const effective = Math.max(0, principal - offset);
      const r = annualRate / 100 / 52;
      if (effective <= 0) return 0;
      if (weeklyPayment <= effective * r) return Infinity;
      const weeks = -Math.log(1 - effective * r / weeklyPayment) / Math.log(1 + r);
      return weeks / 52;
    }
    function saveState(){ ids.forEach(id => localStorage.setItem('wandina_'+id, $(id).value)); }
    function loadState(){
      ids.forEach(id => {
        const v = localStorage.getItem('wandina_'+id);
        if (v !== null) $(id).value = v;
      });
    }
    function diffDays(a,b){ return Math.floor((b-a)/(1000*60*60*24)); }

    function update(){
      saveState();
      const pporBalance = n('pporBalance');
      const pporRate = n('pporRate');
      const pporRepay = n('pporRepay');
      const offsetNow = n('offsetNow');
      const offsetFloor = n('offsetFloor');
      const ipDebt = n('ipDebt');
      const ipRate = n('ipRate');
      const rentW = n('rentWeekly');
      const otherCosts = n('otherCosts');
      const deprAnnual = n('deprAnnual');
      const taxRate = n('taxRate') / 100;
      const salePrice = n('salePrice');
      const sellCostPct = n('sellCostPct') / 100;
      const taxCostBase = n('taxCostBase');
      const capWorksClaimed = n('capWorksClaimed');
      const acqDate = new Date($('acqDate').value);
      const saleContractDate = new Date($('saleContractDate').value);
      const offsetInjectionPct = n('offsetInjectionPct') / 100;

      const ipInterestAnnual = ipDebt * ipRate / 100;
      const ipInterestW = ipInterestAnnual / 52;
      const rentAnnual = rentW * 52;
      const cashCostsAnnual = otherCosts;
      const pretaxAnnual = rentAnnual - ipInterestAnnual - cashCostsAnnual;
      const pretaxW = pretaxAnnual / 52;
      const taxableAnnual = rentAnnual - ipInterestAnnual - cashCostsAnnual - deprAnnual;
      const taxBenefitAnnual = taxableAnnual < 0 ? Math.abs(taxableAnnual) * taxRate : 0;
      const aftertaxAnnual = pretaxAnnual + taxBenefitAnnual;
      const aftertaxW = aftertaxAnnual / 52;
      const paygW = taxBenefitAnnual / 52;

      $('mIpInterestW').textContent = money1(ipInterestW);
      $('mPretaxW').textContent = money1(pretaxW);
      $('mAftertaxW').textContent = money1(aftertaxW);
      $('mPaygW').textContent = money1(paygW);

      const statusBar = $('statusBar');
      statusBar.innerHTML = '';
      const pills = [];
      if (offsetNow < offsetFloor) pills.push(['red','Offset below floor']);
      else pills.push(['green','Offset above floor']);
      if (aftertaxW <= -100) pills.push(['red','IP drag high']);
      else if (aftertaxW < 0) pills.push(['amber','IP drag manageable']);
      else pills.push(['green','IP cashflow positive']);
      pills.push(['blue', `Guarantee at $${rentW}/wk`]);
      pills.forEach(([c,t])=>{ const d=document.createElement('div'); d.className='pill '+c; d.textContent=t; statusBar.appendChild(d); });

      // CGT and sale proceeds
      const sellingCosts = salePrice * sellCostPct;
      const adjustedCostBase = taxCostBase - capWorksClaimed + sellingCosts;
      const grossCapitalGain = salePrice - adjustedCostBase;
      const daysHeld = diffDays(acqDate, saleContractDate);
      const discountEligible = daysHeld >= 365;
      const taxableGain = grossCapitalGain > 0 ? (discountEligible ? grossCapitalGain * 0.5 : grossCapitalGain) : 0;
      const cgt = taxableGain * taxRate;
      const netSaleAfterCosts = salePrice - sellingCosts;
      const netCashAfterDebtTax = netSaleAfterCosts - ipDebt - Math.max(0,cgt);
      const cashToOffset = Math.max(0, netCashAfterDebtTax * offsetInjectionPct);
      const annualInterestSaved = cashToOffset * pporRate / 100;
      $('mDiscountStatus').textContent = discountEligible ? 'Discount yes' : 'Discount no';
      if (discountEligible) {
        $('mDiscountDays').textContent = `${daysHeld} days held by contract date`;
      } else {
        $('mDiscountDays').textContent = `${365 - daysHeld} days short of discount`;
      }
      $('mCgt').textContent = money1(Math.max(0,cgt));
      $('mNetCash').textContent = money1(netCashAfterDebtTax);
      $('mInterestSaved').textContent = money1(annualInterestSaved);

      let saleAdvice = [];
      if (!discountEligible) saleAdvice.push('Do not sign the sale contract before the 12-month threshold unless you are being paid enough to justify losing the 50% CGT discount.');
      if (aftertaxW > -40) saleAdvice.push('Because the guaranteed rent makes the hold cost manageable, you have more negotiating power on timing.');
      if (netCashAfterDebtTax > 0) saleAdvice.push('A sale at this number would release real offset ammunition instead of just shuffling debt around.');
      if (grossCapitalGain <= 0) saleAdvice.push('At this input set, there is no taxable capital gain. Check whether your tax cost base is understated or whether the target sale price is too low.');
      $('saleAdvice').innerHTML = saleAdvice.join(' ');

      // PPOR acceleration
      const baseYears = yearsToPayoff(pporBalance, pporRate, pporRepay, offsetNow);
      const offsetAfter = offsetNow + cashToOffset;
      const newYears = yearsToPayoff(pporBalance, pporRate, pporRepay, offsetAfter);
      const yearsCut = isFinite(baseYears) && isFinite(newYears) ? Math.max(0, baseYears - newYears) : 0;
      $('mBaseYears').textContent = isFinite(baseYears) ? baseYears.toFixed(1) + 'y' : 'n/a';
      $('mNewYears').textContent = isFinite(newYears) ? newYears.toFixed(1) + 'y' : 'n/a';
      $('mYearsCut').textContent = yearsCut.toFixed(1) + 'y';
      $('mOffsetAfter').textContent = money1(offsetAfter);
      $('pporAdvice').innerHTML = yearsCut >= 5
        ? 'This sale setup meaningfully accelerates the PPOR mission. You are not shaving months; you are potentially removing years.'
        : 'At this sale setup, the acceleration is modest. That usually means either the sale price is not high enough, tax is biting too hard, or too little cash is being routed into offset.';

      // Trigger readout
      const sellZone = salePrice >= 780000;
      const marketSoft = false;
      let trigger = '';
      if (!discountEligible || salePrice < 720000) {
        trigger = 'GREEN: hold. The discount timing or the price is not good enough yet.';
      } else if (salePrice >= 720000 && salePrice < 780000) {
        trigger = 'AMBER: get sale-ready but do not rush. Tighten comps and wait for stronger economics unless risk increases.';
      } else if (sellZone && discountEligible) {
        trigger = 'RED: your numbers are in the execution zone. If market momentum is flattening, this is where you harvest equity and attack the PPOR.';
      }
      $('triggerReadout').textContent = trigger;
    }

    loadState();
    ids.forEach(id => $(id).addEventListener('input', update));
    update();
  </script>
</body>
</html>
