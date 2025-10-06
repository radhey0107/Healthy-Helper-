<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <title>Healthy Helper — Healthcare Awareness</title>
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <style>
    :root{
      --accent:#2a9df4;  /* professional healthcare blue */
      --bg:#f4f9fc;
      --card:#ffffff;
      --text:#033f5d;
    }
    body{font-family:"Segoe UI",Arial,sans-serif;margin:0;background:var(--bg);color:var(--text);}
    header{background:var(--accent);color:#fff;padding:25px;text-align:center;}
    header h1{margin:0;font-size:28px;}
    nav{display:flex;flex-wrap:wrap;justify-content:center;background:#d6eef9;padding:10px;gap:8px;}
    nav button{border:none;padding:10px 14px;border-radius:6px;background:#fff;color:var(--accent);font-weight:bold;cursor:pointer;}
    nav button.active{background:var(--accent);color:#fff;}
    .page{display:none;padding:20px;}
    .card{background:var(--card);padding:18px;border-radius:10px;box-shadow:0 3px 8px rgba(0,0,0,0.08);margin-bottom:16px;}
    h2{margin-top:0;color:var(--accent);}
    h3{color:#1c6db3;}
    .chip{display:inline-block;padding:6px 10px;margin:5px;border:1px solid #ccc;border-radius:20px;cursor:pointer;}
    .chip.sel{background:var(--accent);color:#fff;}
  .chip{transition:transform .12s ease,box-shadow .12s ease}
  .chip:hover{transform:translateY(-3px);box-shadow:0 6px 14px rgba(42,157,244,0.18)}
  .chip.sel{box-shadow:0 6px 18px rgba(2,90,150,0.18)}
  .progress{height:10px;background:#e6f5ff;border-radius:6px;overflow:hidden;margin-top:6px}
  .progress > div{height:100%;background:linear-gradient(90deg,var(--accent),#1c6db3);width:0%;transition:width .6s ease}
    input,select,textarea,button{padding:10px;margin:6px 0;border-radius:6px;border:1px solid #ccc;font-size:15px;}
    textarea{width:100%;}
    button.primary{background:var(--accent);color:#fff;border:none;cursor:pointer;}
    button.danger{background:#c62828;color:#fff;border:none;}
    .result{margin-top:10px;padding:10px;border-radius:6px;background:#f0f9ff;border:1px solid #b3e0ff;}
  .error{color:#c62828;font-size:13px;margin-top:4px;display:none}
    table{width:100%;border-collapse:collapse;margin-top:8px;}
    th,td{border:1px solid #ddd;padding:6px;text-align:left;font-size:14px;}
    th{background:#f8faff;}
    footer{background:#033f5d;color:#fff;text-align:center;padding:18px;margin-top:20px;font-size:14px;}
    a{color:var(--accent);}
  /* Government schemes styling */
  .scheme-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(260px,1fr));gap:12px;margin-top:8px}
  .scheme{background:#fff;border-radius:10px;padding:12px;border:1px solid #e6f3fb}
  .scheme h4{margin:0;color:var(--accent);font-size:16px}
  .badge{display:inline-block;padding:4px 8px;border-radius:12px;background:#eef7ff;color:var(--accent);font-weight:600;margin-top:6px;font-size:12px}
  .muted{color:#556;font-size:13px}
  /* Dashboard styles */
  .kpi-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(180px,1fr));gap:12px;margin-top:12px}
  .kpi{background:#fff;padding:12px;border-radius:8px;border:1px solid #eaf6ff}
  .kpi-title{font-size:13px;color:#667}
  .kpi-value{font-size:22px;font-weight:700;color:var(--accent);margin-top:6px}
  .kpi-note{font-size:12px;color:#556;margin-top:6px}
    .chart-card canvas{max-width:100%;height:auto}
    .chart-row{display:grid;grid-template-columns:1fr 1fr;gap:14px;margin-top:14px;align-items:start}
    @media (max-width:700px){
      .chart-row{grid-template-columns:1fr;}
    }
    /* Tooltip for charts */
    .chart-tooltip{position:fixed;z-index:9999;padding:8px 10px;border-radius:6px;background:var(--card);color:var(--text);box-shadow:0 6px 18px rgba(0,0,0,0.12);font-size:13px;display:none;pointer-events:none}
    /* Toast notifications */
    .toast{position:fixed;right:18px;bottom:18px;background:#033f5d;color:#fff;padding:10px 14px;border-radius:8px;box-shadow:0 8px 24px rgba(3,63,93,0.28);z-index:10000;opacity:0;transform:translateY(8px);transition:opacity .26s,transform .26s}
    .toast.show{opacity:1;transform:translateY(0)}
    /* small icon next to headings */
    .hicon{width:18px;height:18px;vertical-align:middle;margin-right:8px;opacity:0.95}
  </style>
</head>
<body>
  <header>
    <h1>Healthy Helper</h1>
    <p>Your trusted partner in healthcare awareness & prevention</p>
  </header>

  <!-- Navigation -->
  <nav id="nav">
    <button data-page="home" class="active">Home</button>
    <button data-page="diseases">Diseases</button>
    <button data-page="prevent">Prevention</button>
    <button data-page="symptom">Symptom Checker</button>
    <button data-page="bmi">BMI Calculator</button>
    <button data-page="survey">Survey</button>
    <button data-page="govt">Govt Schemes</button>
    <button data-page="credits">Credits</button>
  </nav>

  <!-- Home (Dashboard) -->
  <section id="page-home" class="page" style="display:block;">
    <div class="card">
      <h2>Dashboard — Healthy Helper Overview</h2>
      <p>At-a-glance view of chronic disease burden and awareness. Data below uses survey responses when available; otherwise illustrative national estimates are shown.</p>

      <div class="kpi-grid">
        <div class="kpi">
          <div class="kpi-title">Estimated adults with ≥1 chronic disease</div>
          <div class="kpi-value" id="kpi-prevalence">—</div>
          <div class="kpi-note">% of adults (estimate)</div>
        </div>
        <div class="kpi">
          <div class="kpi-title">Most common condition</div>
          <div class="kpi-value" id="kpi-top">—</div>
          <div class="kpi-note">By share among affected</div>
        </div>
        <div class="kpi">
          <div class="kpi-title">Awareness among affected</div>
          <div class="kpi-value" id="kpi-aware">—</div>
          <div class="kpi-note">% who know they have a condition</div>
        </div>
        <div class="kpi">
          <div class="kpi-title">Survey responses</div>
          <div class="kpi-value" id="kpi-resp">0</div>
          <div class="kpi-note">Local survey data points</div>
        </div>
      </div>

  <div class="chart-row">
        <div class="card chart-card">
          <h3 style="margin-top:0">Chronic diseases — distribution</h3>
          <canvas id="chartDiseases" width="320" height="240"></canvas>
          <div id="legendDiseases" style="margin-top:8px;font-size:13px"></div>
        </div>

        <div class="card chart-card">
          <h3 style="margin-top:0">Awareness among people with chronic disease</h3>
          <canvas id="chartAware" width="320" height="240"></canvas>
          <div id="legendAware" style="margin-top:8px;font-size:13px"></div>
        </div>
      </div>

    </div>
  </section>

  <!-- Diseases -->
  <section id="page-diseases" class="page">
    <div class="card">
      <h2>Major Chronic Diseases — Quick guide</h2>
      <p>Short, actionable summaries to help you understand, spot early signs, and reduce risk. Click the Prevention tab for general lifestyle guidance.</p>

      <h3>Diabetes — at a glance</h3>
      <ul>
        <li><b>What it is:</b> High blood sugar due to insulin resistance or low insulin production.</li>
        <li><b>Quick facts:</b> Type 2 is most common, often linked to excess weight and inactivity.</li>
        <li><b>Reduce your risk:</b> Achieve/maintain healthy weight, choose whole grains & fiber, limit sugary drinks, and be active most days.</li>
        <li><b>Red flags — see a doctor if:</b> Excessive thirst, unexplained weight loss, wounds that won't heal, or repeated infections.</li>
        <li><b>Daily tip:</b> Carry a small snack if you take diabetes medicines that can lower blood sugar.</li>
      </ul>

      <h3>Hypertension (High blood pressure)</h3>
      <ul>
        <li><b>What it is:</b> Blood pressure consistently higher than normal, increasing heart and stroke risk.</li>
        <li><b>Quick facts:</b> Often symptomless — called the 'silent killer'. Regular checks are essential.</li>
        <li><b>Reduce your risk:</b> Cut salt, eat potassium-rich foods (fruits/veg), lose excess weight, limit alcohol, and be active.</li>
        <li><b>Red flags — see a doctor if:</b> Very high readings (e.g., &gt;180/120), severe headache, chest pain, or visual changes.</li>
        <li><b>Daily tip:</b> Keep a BP log; many pharmacies offer free checks if you don't have a home monitor.</li>
      </ul>

      <h3>Heart disease (Coronary artery disease & related)</h3>
      <ul>
        <li><b>What it is:</b> Narrowing or blockage of the heart's blood vessels leading to chest pain, heart attack, or heart failure.</li>
        <li><b>Quick facts:</b> Risk rises with smoking, high BP, high cholesterol, diabetes and sedentary lifestyle.</li>
        <li><b>Reduce your risk:</b> Stop tobacco, control BP/cholesterol/diabetes, eat healthy fats (nuts, fish), and exercise regularly.</li>
        <li><b>Red flags — seek urgent care if:</b> New chest pain, pressure, shortness of breath, fainting, or sudden sweating and nausea.</li>
        <li><b>Daily tip:</b> Learn Hands-Only CPR and keep emergency numbers handy in case of sudden events.</li>
      </ul>

      <h3>COPD (Chronic Obstructive Pulmonary Disease)</h3>
      <ul>
        <li><b>What it is:</b> Long-term lung disease causing airflow limitation—includes chronic bronchitis and emphysema.</li>
        <li><b>Quick facts:</b> Smoking is the leading cause; air pollution and workplace exposures also contribute.</li>
        <li><b>Reduce your risk:</b> Quit smoking (best single step), avoid polluted air, use masks where needed, and get vaccinated for flu/pneumonia.</li>
        <li><b>Red flags — see a doctor if:</b> Worsening cough, increasing sputum, breathlessness at rest, or frequent chest infections.</li>
        <li><b>Daily tip:</b> Pace activities and use pursed-lip breathing to help with breathlessness during exertion.</li>
      </ul>

      <h3>CKD (Chronic Kidney Disease)</h3>
      <ul>
        <li><b>What it is:</b> Gradual loss of kidney function; early stages may have no symptoms.</li>
        <li><b>Quick facts:</b> Diabetes and hypertension are the most common causes; early detection slows progression.</li>
        <li><b>Reduce your risk:</b> Control blood sugar and blood pressure, avoid unnecessary painkillers, stay hydrated but follow your doctor's advice if you have kidney disease.</li>
        <li><b>Red flags — see a doctor if:</b> Persistent swelling in legs/around eyes, foamy urine, decreased urine output, or unexplained fatigue.</li>
        <li><b>Daily tip:</b> Keep an up-to-date list of medications and supplements — some affect the kidneys and may need dose adjustment.</li>
      </ul>
    </div>
  </section>

  <!-- Prevention -->
  <section id="page-prevent" class="page">
    <div class="card">
      <h2>Preventive Measures</h2>
      <p>Simple, practical and evidence-based actions you can take to reduce the risk of chronic disease and maintain everyday wellbeing. Where useful, targets and examples are provided.</p>
      <ul>
        <li><strong>Healthy eating</strong>
          <ul>
            <li>Follow a plate-based approach: half vegetables & fruit, one-quarter whole grains, one-quarter lean protein. Example: a plate with mixed salad, brown rice, and grilled fish.</li>
            <li>Limit salt to &lt;5 g/day (about 1 teaspoon). Use herbs, spices and citrus to flavour food instead of salt.</li>
            <li>Limit free sugars to &lt;10% of daily calories (avoid sugary drinks; prefer water, unsweetened tea/coffee).</li>
            <li>Prefer minimally processed foods — canned pulses, frozen vegetables and plain yogurt are good, affordable options.</li>
            <li>Plan meals and use portion control: measure oil (1 tbsp ≈ 14 g), fill smaller plates, and avoid late-night heavy meals.</li>
          </ul>
        </li>

        <li><strong>Physical activity</strong>
          <ul>
            <li>Aim for at least 150 minutes/week of moderate-intensity aerobic activity (e.g., brisk walking 30 minutes × 5 days) or 75 minutes of vigorous activity.</li>
            <li>Include two sessions/week of muscle-strengthening activities (bodyweight exercises, resistance bands, or weights).</li>
            <li>Build activity into your day: take stairs, cycle for short trips, or do 10-minute exercise 'snacks' if you can't do a full session.</li>
            <li>If mobility is limited, focus on chair-based exercises, flexibility and balance training to prevent falls (especially for older adults).</li>
          </ul>
        </li>

        <li><strong>Tobacco and alcohol</strong>
          <ul>
            <li>Stop tobacco in any form — smoking, chewing or vaping. Proven supports include brief advice from a health worker, nicotine replacement (patch/gum) and behavioural counselling; ask your provider about local quit services.</li>
            <li>If you use alcohol, follow low-risk limits (check local guidance). Avoid binge drinking (4+ drinks for women or 5+ for men in a single session) and consider alcohol-free days.</li>
          </ul>
        </li>

        <li><strong>Mental health, stress and sleep</strong>
          <ul>
            <li>Practice simple stress-management daily: 5–10 minutes of deep breathing, progressive muscle relaxation or short mindfulness exercises.</li>
            <li>Aim for 7–9 hours of sleep for adults; keep a consistent bedtime, reduce screens before sleep and create a calm sleep environment.</li>
            <li>Seek help early for anxiety, depression or substance use — community mental health services and helplines can provide support.</li>
          </ul>
        </li>

        <li><strong>Regular checks, screening & self-care</strong>
          <ul>
            <li>Know basic targets: normal BP &lt;130/80 mmHg (discuss individualized targets with your clinician), fasting blood sugar &lt;100 mg/dL, and cholesterol goals based on risk.</li>
            <li>Adults should check BP at least once a year (more often if high), and those with risk factors should have blood sugar and lipid checks as advised.</li>
            <li>Follow age- and risk-based cancer screening (cervical, breast and colorectal) according to national guidelines — ask your provider about timing and tests available locally.</li>
            <li>Learn self-examination where appropriate (breast awareness, testicular checks) and report persistent changes promptly.</li>
          </ul>
        </li>

        <li><strong>Vaccination & infection prevention</strong>
          <ul>
            <li>Keep routine vaccines up to date (influenza yearly, tetanus boosters, and others recommended by national schedules). Vaccination reduces severe illness and complications.</li>
            <li>Practice good hand hygiene, safe food handling and timely care for infections to reduce disease spread and complications.</li>
          </ul>
        </li>

        <li><strong>Medication safety & environmental risks</strong>
          <ul>
            <li>Take medicines exactly as prescribed; carry an up-to-date list of medicines and allergies. Review long-term drugs periodically with your doctor or pharmacist.</li>
            <li>Avoid unnecessary or frequent use of NSAIDs/painkillers without medical advice — they can harm kidneys and stomach lining when overused.</li>
            <li>Reduce indoor air pollution (ventilation when cooking, avoid burning waste), and use protective equipment at work to limit occupational exposures.</li>
          </ul>
        </li>

        <li><strong>Community resources & healthy environments</strong>
          <ul>
            <li>Use government screening camps, community health workers and scheme benefits for free/low-cost services (vaccines, check-ups, medicines).</li>
            <li>Join local groups for walking, cooking classes or chronic disease self-management — peer support improves adherence to healthy behaviours.</li>
          </ul>
        </li>

        <li><strong>When to seek urgent care</strong>
          <ul>
            <li>Seek immediate medical help for chest pain, sudden breathlessness, sudden weakness or slurred speech, severe bleeding, loss of consciousness or other red-flag symptoms.</li>
            <li>For non-urgent but concerning symptoms (persistent pain, unexplained weight loss, ongoing fever), arrange timely primary care follow-up — early assessment improves outcomes.</li>
          </ul>
        </li>

        <li><strong>Special populations</strong>
          <ul>
            <li>Older adults: focus on fall prevention (home safety, strength & balance exercises), medication review and vaccination (influenza, pneumococcal where indicated).</li>
            <li>Pregnant people: attend prenatal visits, follow nutrition and supplementation advice (iron, folic acid), and get recommended vaccinations.</li>
            <li>People with diabetes: regular foot care, annual eye checks, and individualized targets for glucose and blood pressure to reduce complications.</li>
          </ul>
        </li>
      </ul>
    </div>
  </section>

  <!-- Symptom Checker -->
  <section id="page-symptom" class="page">
    <div class="card">
      <h2>Symptom Checker</h2>
      <p>Select the symptoms you have. This tool gives quick, non-diagnostic suggestions and points you to related information.</p>
      <label>Search symptoms</label><br>
      <input id="symFilter" placeholder="Type to filter symptoms (e.g., cough, pain)"><br>
      <div id="symptomsList" aria-live="polite" style="margin-top:8px"></div>
      <div style="margin-top:10px;display:flex;gap:8px;flex-wrap:wrap;align-items:center">
        <button id="checkSymptoms" class="primary">Check</button>
        <button id="clearSymptoms" class="danger">Clear</button>
        <div style="margin-left:auto;color:#666;font-size:13px">Selected: <span id="selCount">0</span></div>
      </div>
      <div id="symResult" class="result" style="display:none;margin-top:12px;padding:12px"></div>
    </div>
  </section>

  <!-- BMI -->
  <section id="page-bmi" class="page">
    <div class="card">
      <h2>BMI Calculator</h2>
      <p><b>What is BMI?</b> Body Mass Index (BMI) is a simple number calculated from height and weight that gives an estimate of body fat for most adults. It helps identify healthy and unhealthy weight ranges for population-level guidance.</p>
      <div style="display:flex;gap:20px;flex-wrap:wrap;align-items:flex-start">
        <div style="flex:1;min-width:220px">
          <label>Height (cm):</label><br>
          <input type="number" id="height" placeholder="e.g. 170"><br>
          <label>Weight (kg):</label><br>
          <input type="number" id="weight" placeholder="e.g. 70"><br>
          <div style="display:flex;gap:8px;margin-top:8px">
            <button id="calcBmi" class="primary">Calculate</button>
            <button id="clearBmi" class="danger">Clear</button>
          </div>
        </div>
        <div style="flex:1;min-width:260px">
          <div style="padding:10px;background:#fff;border-radius:8px;box-shadow:0 2px 8px rgba(0,0,0,0.04)">
            <div style="font-weight:bold;color:#055">BMI ranges</div>
            <ul style="margin:6px 0 0 16px;color:#334">
              <li><b>Underweight:</b> BMI &lt; 18.5 — may indicate malnutrition or underlying illness.</li>
              <li><b>Healthy/Normal:</b> BMI 18.5–24.9 — associated with lowest average health risk.</li>
              <li><b>Overweight:</b> BMI 25.0–29.9 — increased risk for some conditions; lifestyle changes advised.</li>
              <li><b>Obese:</b> BMI ≥ 30 — higher risk of diabetes, heart disease, and other problems; seek medical advice.</li>
            </ul>
            <div style="font-size:13px;color:#666;margin-top:8px">Note: BMI is a screening tool and may not reflect body composition (muscle vs fat). Use it with other health indicators.</div>
          </div>
        </div>
      </div>
      <div id="bmiResult" class="result" style="display:none;margin-top:12px;padding:14px"></div>
    </div>
  </section>

  <!-- Survey -->
  <section id="page-survey" class="page">
    <div class="card">
      <h2>Health Survey</h2>
      <p>All responses are stored locally in your browser. Exportable to CSV.</p>
      <label><input type="checkbox" id="consent"> I consent to participate</label> <span id="err-consent" class="error">Consent is required to submit</span><br>
      <label for="name">Name</label>
      <input type="text" id="name"><span id="err-name" class="error">Please enter your name or leave blank to remain anonymous</span>
      <label for="age">Age Group <span style="font-size:13px;color:#666">(required)</span></label>
      <select id="age"><option value="">Select</option><option>&lt;18</option><option>18-30</option><option>31-45</option><option>46-60</option><option>&gt;60</option></select><span id="err-age" class="error">Please select an age group</span>
      <label for="gender">Gender <span style="font-size:13px;color:#666">(required)</span></label>
      <select id="gender"><option value="">Select</option><option>Male</option><option>Female</option><option>Other</option></select><span id="err-gender" class="error">Please select gender</span>
      <label>Do you have any diagnosed chronic disease?</label>
      <select id="disease"><option value="">Select</option><option>None</option><option>Diabetes</option><option>Hypertension</option><option>Heart Disease</option><option>CKD</option><option>COPD</option></select>
      <label>Do you have health insurance?</label>
      <select id="insurance"><option value="">Select</option><option>Yes - Govt</option><option>Yes - Private</option><option>No</option></select>
      <label>Are you aware of government schemes?</label>
      <select id="aware"><option value="">Select</option><option>Yes</option><option>No</option><option>Not Sure</option></select>
      <label>Any additional comments</label><textarea id="comments"></textarea><br>
      <div style="display:flex;gap:8px;align-items:center">
        <button id="submitSurvey" class="primary">Submit</button>
        <button id="viewSurvey">View Responses</button>
        <button id="exportCsv">Export CSV</button>
        <label style="margin-left:8px"><input type="checkbox" id="exportAnon"> Export anonymized</label>
        <button id="clearForm" class="danger">Clear Form</button>
      </div>
      <div id="surveyMsg" class="result" style="display:none;margin-top:10px;"></div>
    </div>
  </section>

  <!-- Govt Schemes -->
  <section id="page-govt" class="page">
    <div class="card">
      <h2>Government Schemes — How they help</h2>
      <p>Key public programmes you can use for screening, treatment, medicines and digital health records. Click a card for quick eligibility, benefits and how to apply.</p>
      <div class="scheme-grid">
        <div class="scheme">
          <h4>Ayushman Bharat (PMJAY)</h4>
          <div class="badge">Health insurance</div>
          <p class="muted">Cashless secondary & tertiary treatment for eligible families (cover up to ₹5 lakh/year).</p>
          <p><b>Who benefits:</b> Economically vulnerable families (check official list by state).</p>
          <p><b>How to apply:</b> Visit the official portal or your local health centre; many hospitals accept PMJAY cards at admission.</p>
          <p><a href="https://pmjay.gov.in" target="_blank">Official site & resources</a></p>
        </div>

        <div class="scheme">
          <h4>Jan Aushadhi (Pradhan Mantri Bhartiya Janaushadhi Pariyojana)</h4>
          <div class="badge">Affordable medicines</div>
          <p class="muted">Subsidised generic medicines available at Janaushadhi Kendras — same active ingredient at lower cost.</p>
          <p><b>Tip:</b> Ask your doctor for generic equivalents and check the nearest Janaushadhi store.</p>
          <p><a href="https://janaushadhi.gov.in/" target="_blank">Find stores & price list</a></p>
        </div>

        <div class="scheme">
          <h4>ABHA (Digital Health ID)</h4>
          <div class="badge">Digital records</div>
          <p class="muted">Create a Health ID to link medical records, lab reports and prescriptions securely across providers.</p>
          <p><b>Benefits:</b> Easier referrals, reduced paperwork, faster emergency care when records are accessible.</p>
          <p><a href="https://healthid.ndhm.gov.in/" target="_blank">Register for ABHA</a></p>
        </div>

        <div class="scheme">
          <h4>E-Sanjeevani (Telemedicine)</h4>
          <div class="badge">Remote consults</div>
          <p class="muted">Free teleconsultations provided by public health facilities — useful for follow-ups, triage and specialist advice.</p>
          <p><b>How to use:</b> Book via the portal or ask your local PHC for the link; keep your medical history and medicines list ready.</p>
          <p><a href="https://esanjeevani.in/" target="_blank">Use E-Sanjeevani</a></p>
        </div>

        <div class="scheme">
          <h4>NPCDCS (NCD programme)</h4>
          <div class="badge">Prevention & screening</div>
          <p class="muted">National Programme for Prevention & Control of Cancer, Diabetes, CVD and Stroke — supports screening camps and NCD clinics.</p>
          <p><b>Where to go:</b> Primary Health Centres and Community Health Centres often run screening days — check local health office calendars.</p>
          <p><a href="https://nhm.gov.in/" target="_blank">Programme details</a></p>
        </div>

        <div class="scheme">
          <h4>Pradhan Mantri Jan Arogya Yojana (additional resources)</h4>
          <div class="badge">Support services</div>
          <p class="muted">Information on empanelled hospitals, grievance redressal and helplines related to public health schemes.</p>
          <p><a href="https://pmjay.gov.in/" target="_blank">Hospital list & help</a></p>
        </div>
      </div>

      <div style="margin-top:12px">
        <h3 style="margin-bottom:6px;color:var(--accent)">Quick tips</h3>
        <ul>
          <li>Carry any ID and Ration/SECC details when applying for benefits — many schemes use these to verify eligibility.</li>
          <li>Keep digital copies (ABHA) or printed copies of important medical records and prescriptions.</li>
          <li>Ask about referral processes and what documents hospitals require to use insurance schemes.</li>
          <li>If unsure, call the national helpline numbers listed on official sites before visiting a hospital to confirm coverage and documents needed.</li>
        </ul>
      </div>
    </div>
  </section>

  <!-- Credits -->
  <section id="page-credits" class="page">
    <div class="card">
      <h2>Credits</h2>
      <p>This project was created as part of the Community Engagement Project — <b>Health Awareness Drive</b>.</p>
      <h3>Team members</h3>
      <ul>
        <li>Sushrut Mahajan</li>
        <li>Sahil Khandare</li>
        <li>Pranavee More</li>
        <li>Samruddhi Kale</li>
      </ul>
      <p class="muted">Thank you to everyone who contributed their time, feedback, and testing. This is an educational tool and not a substitute for professional medical advice.</p>
    </div>
  </section>

  <footer>
    Healthy Helper © 2025 | Awareness & Prevention Platform | Not a substitute for medical advice
  </footer>

  <script>
    // NAVIGATION
    document.querySelectorAll("nav button").forEach(btn=>{
      btn.addEventListener("click",()=>{
        document.querySelectorAll("nav button").forEach(b=>b.classList.remove("active"));
        document.querySelectorAll(".page").forEach(p=>p.style.display="none");
        document.getElementById("page-"+btn.dataset.page).style.display="block";
        btn.classList.add("active");
      });
    });

  // SYMPTOM CHECKER
  const diseases={
      "Diabetes":["Increased thirst","Frequent urination","Slow healing wounds","Blurred vision","Fatigue","Unexplained weight loss","Tingling or numbness in hands or feet","Increased hunger","Frequent infections"],
      "Hypertension":["Headache","Dizziness","High blood pressure","Nosebleeds","Shortness of breath","Vision changes","Facial flushing"],
      "Heart Disease":["Chest pain","Shortness of breath","Swelling in feet","Palpitations","Fainting or near-fainting","Excessive sweating","Nausea or indigestion","Pain radiating to jaw/arm"],
      "COPD":["Persistent cough","Breathlessness","Chest tightness","Wheezing","Increased sputum","Frequent chest infections","Reduced exercise tolerance"],
      "CKD":["Swelling","Fatigue","Frequent urination at night","Itchy skin","Loss of appetite","Nausea","Changes in urine colour","Muscle cramps"]
    };
    const allSymptoms=Array.from(new Set([].concat(...Object.values(diseases)))).sort();
    const symDiv=document.getElementById("symptomsList");
    const selCount=document.getElementById("selCount");

    function renderChips(filter=""){
      symDiv.innerHTML="";
      allSymptoms.filter(s=>s.toLowerCase().includes(filter.toLowerCase())).forEach(sym=>{
        let chip=document.createElement("div");
        chip.textContent=sym;chip.className="chip";
        chip.onclick=()=>{chip.classList.toggle("sel"); updateSelCount();};
        symDiv.appendChild(chip);
      });
    }
    function updateSelCount(){selCount.textContent=document.querySelectorAll(".chip.sel").length}

    renderChips();
    document.getElementById("symFilter").addEventListener("input",(e)=>renderChips(e.target.value));

    const adviceMap={
      "Diabetes":"Keep hydrated, reduce simple carbs, and check blood sugar if you have risk factors.",
      "Hypertension":"Reduce salt, check BP, and seek evaluation if you have headaches or high readings.",
      "Heart Disease":"If chest pain or shortness of breath appear, seek emergency care immediately.",
      "COPD":"Avoid smoke and pollution; use inhalers as prescribed and get flu vaccination.",
      "CKD":"Avoid unnecessary painkillers and get kidney function tests if you have diabetes or high BP."
    };

    function createResultNode(name,pct){
      let wrap=document.createElement('div');
      wrap.style.marginBottom='10px';
      let title=document.createElement('div');title.innerHTML='<b>'+name+'</b> — <span style="color:#1c6db3">'+pct+'%</span> match';
      let prog=document.createElement('div');prog.className='progress';let bar=document.createElement('div');bar.style.width=pct+'%';prog.appendChild(bar);
      let adv=document.createElement('div');adv.style.marginTop='6px';adv.style.color='#334';adv.textContent=adviceMap[name]||'';
      let link=document.createElement('a');link.href='#page-diseases';link.textContent=' Read more';link.style.marginLeft='8px';
      link.onclick=(e)=>{e.preventDefault();document.getElementById('page-diseases').scrollIntoView({behavior:'smooth'});};
      adv.appendChild(link);
      wrap.appendChild(title);wrap.appendChild(prog);wrap.appendChild(adv);
      return wrap;
    }

    // small icons injector for section headings
    function addHeadingIcons(){
      const icons={
        'page-diseases':'<svg class="hicon" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg"><circle cx="12" cy="7" r="3" stroke="currentColor" stroke-width="1.2"/><path d="M5 20c1.8-3 5.2-5 7-5s5.2 2 7 5" stroke="currentColor" stroke-width="1.2" stroke-linecap="round" stroke-linejoin="round"/></svg>',
        'page-prevent':'<svg class="hicon" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg"><path d="M12 2v6" stroke="currentColor" stroke-width="1.2" stroke-linecap="round"/><path d="M5 8c3-1 6-1 7 0 1-1 4-1 7 0" stroke="currentColor" stroke-width="1.2" stroke-linecap="round"/></svg>',
        'page-survey':'<svg class="hicon" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg"><rect x="3" y="4" width="18" height="14" rx="2" stroke="currentColor" stroke-width="1.2"/><path d="M7 8h10" stroke="currentColor" stroke-width="1.2" stroke-linecap="round"/></svg>',
        'page-govt':'<svg class="hicon" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg"><path d="M12 2l8 4-8 4-8-4 8-4z" stroke="currentColor" stroke-width="1.2"/><path d="M4 10v6a2 2 0 0 0 2 2h12" stroke="currentColor" stroke-width="1.2"/></svg>'
      };
      Object.entries(icons).forEach(([id,svg])=>{
        const el=document.getElementById(id); if(!el) return; const h=el.querySelector('h2')||el.querySelector('h3')||el.querySelector('h4'); if(h) h.innerHTML=svg + h.innerHTML;
      });
    }
    addHeadingIcons();

    // tooltip element
    const tooltip=document.createElement('div');tooltip.className='chart-tooltip';document.body.appendChild(tooltip);

    // simple toast
    function showToast(msg,timeout=2600){
      let t=document.createElement('div');t.className='toast';t.textContent=msg;document.body.appendChild(t);
      setTimeout(()=>t.classList.add('show'),20);
      setTimeout(()=>{t.classList.remove('show');setTimeout(()=>t.remove(),300)},timeout);
    }

    document.getElementById("checkSymptoms").onclick=()=>{
      let selected=[...document.querySelectorAll(".chip.sel")].map(c=>c.textContent);
      if(!selected.length){alert("Select at least one symptom");return;}
      let results=[];
      for(let [dis,symList] of Object.entries(diseases)){
        let match=selected.filter(s=>symList.includes(s)).length;
        if(match>0){let pct=Math.round((match/symList.length)*100);results.push({dis,pct});}
      }
      let resDiv=document.getElementById("symResult");resDiv.style.display="block";resDiv.innerHTML="";
      if(!results.length){resDiv.innerHTML="No matches found. Consider seeing a healthcare provider for persistent symptoms.";return}
      let header=document.createElement('div');header.innerHTML='<b>Possible conditions (ranked)</b>';
      resDiv.appendChild(header);
      results.sort((a,b)=>b.pct-a.pct).forEach(r=>resDiv.appendChild(createResultNode(r.dis,r.pct)));
    };

    document.getElementById("clearSymptoms").onclick=()=>{
      document.querySelectorAll(".chip.sel").forEach(c=>c.classList.remove("sel"));
      document.getElementById("symResult").style.display="none";document.getElementById('symFilter').value='';renderChips();updateSelCount();
    };

    // BMI
    document.getElementById("calcBmi").onclick=()=>{
      let h=document.getElementById("height").value;
      let w=document.getElementById("weight").value;
      if(!h||!w){alert("Enter both height and weight");return;}
      h=h/100;let bmi=w/(h*h);
      let cat, color, advice;
      if(bmi<18.5){cat='Underweight'; color='#3ea6ff'; advice='Consider a balanced, calorie-dense diet and check for underlying causes.'}
      else if(bmi<25){cat='Healthy (Normal)'; color='#2bb673'; advice='Great — maintain a balanced diet and regular activity to stay healthy.'}
      else if(bmi<30){cat='Overweight'; color='#f4a261'; advice='Aim for gradual weight loss via diet and activity; small changes add up.'}
      else {cat='Obese'; color='#e06464'; advice='Higher health risk — discuss weight management options with your healthcare provider.'}

      // compute healthy weight range for this height (BMI 18.5 - 24.9)
      let minHealthy=18.5*(h*h);
      let maxHealthy=24.9*(h*h);
      let pct=Math.max(0,Math.min(100,Math.round((bmi/40)*100)));
      let html='<div style="display:flex;align-items:center;gap:12px;flex-wrap:wrap">'
        +'<div style="flex:1;min-width:180px">Your BMI: <b>'+bmi.toFixed(1)+'</b><br><span style="color:'+color+';font-weight:700">'+cat+'</span></div>'
        +'<div style="flex:2;min-width:180px">'
          +'<div class="progress" aria-hidden="true"><div style="background:'+color+';width:'+pct+'%"></div></div>'
          +'<div style="font-size:13px;color:#444;margin-top:8px">'+advice+'</div>'
        +'</div>'
      +'</div>'
      +'<div style="margin-top:8px;font-size:13px;color:#666"><b>Healthy BMI range:</b> 18.5–24.9. Use BMI with other measures (waist circumference, activity level, blood tests) to assess health.</div>'
      +'<div style="margin-top:8px;font-size:14px;color:#333"><b>Estimated healthy weight for your height ('+Math.round(h*100)+' cm):</b> '+minHealthy.toFixed(1)+' kg — '+maxHealthy.toFixed(1)+' kg.</div>';

      // suggestion
      let suggestion='';
      if(bmi<18.5){
        let target=(minHealthy+maxHealthy)/2;
        suggestion='You are below the healthy range. A reasonable target weight could be about '+target.toFixed(1)+' kg (mid-range).';
      } else if(bmi>24.9){
        let target=maxHealthy; suggestion='You are above the healthy range. A reasonable initial target is to reach '+target.toFixed(1)+' kg (upper healthy limit).';
      } else { suggestion='You are within the healthy weight range. Continue healthy habits to maintain it.' }
      html += '<div style="margin-top:8px;font-size:13px;color:#334">'+suggestion+'</div>';

      let resDiv=document.getElementById("bmiResult");resDiv.style.display='block';resDiv.innerHTML=html;
    };
    document.getElementById("clearBmi").onclick=()=>{
      document.getElementById("height").value="";document.getElementById("weight").value="";
      document.getElementById("bmiResult").style.display="none";
    };

    // SURVEY
    const STORAGE_KEY="healthyhelper_survey";
    function loadResponses(){return JSON.parse(localStorage.getItem(STORAGE_KEY)||"[]");}
    function saveResponses(arr){localStorage.setItem(STORAGE_KEY,JSON.stringify(arr));}
    document.getElementById("submitSurvey").onclick=()=>{
      // inline validation
      let consentEl=document.getElementById("consent"), ageEl=document.getElementById("age"), genderEl=document.getElementById("gender");
      let ok=true;
      document.querySelectorAll('.error').forEach(e=>e.style.display='none');
      if(!consentEl.checked){document.getElementById('err-consent').style.display='inline';ok=false}
      if(!ageEl.value){document.getElementById('err-age').style.display='inline';ok=false}
      if(!genderEl.value){document.getElementById('err-gender').style.display='inline';ok=false}
      if(!ok) return;

      let rec={
        time:new Date().toLocaleString(),
        consent:true,
        name:document.getElementById("name").value.trim(),
        age:ageEl.value,
        gender:genderEl.value,
        disease:document.getElementById("disease").value,
        insurance:document.getElementById("insurance").value,
        aware:document.getElementById("aware").value,
        comments:document.getElementById("comments").value.trim()
      };
      try{
        let arr=loadResponses();arr.push(rec);saveResponses(arr);
        document.getElementById("surveyMsg").style.display="block";
        document.getElementById("surveyMsg").innerHTML="Response saved. Total: "+arr.length;
        updateDashboard(); showToast('Response saved');
      }catch(e){alert('Failed to save response (storage full?)');}
    };
    document.getElementById("viewSurvey").onclick=()=>{
      let arr=loadResponses();let msg=document.getElementById("surveyMsg");
      msg.style.display="block";
      if(!arr.length){msg.innerHTML="No responses yet.";return;}
      // summary counts
      let total=arr.length;let byAge={};let byDisease={};let byInsurance={};
      arr.forEach(r=>{byAge[r.age]=(byAge[r.age]||0)+1;byDisease[r.disease]=(byDisease[r.disease]||0)+1;byInsurance[r.insurance]=(byInsurance[r.insurance]||0)+1});
      let summaryHtml='<div style="margin-bottom:8px"><b>Total:</b> '+total+' &nbsp; <b>By Age:</b> '+Object.entries(byAge).map(e=>e[0]+':'+e[1]).join(', ')+' </div>';
      let html=summaryHtml+"<table><tr><th>#</th><th>Time</th><th>Name</th><th>Age</th><th>Gender</th><th>Disease</th><th>Insurance</th><th>Aware</th><th>Comments</th><th>Action</th></tr>";
      arr.forEach((r,i)=>{
        html+="<tr><td>"+(i+1)+"</td><td>"+r.time+"</td><td>"+(r.name||'<i>anonymous</i>')+"</td><td>"+r.age+"</td><td>"+r.gender+"</td><td>"+r.disease+"</td><td>"+r.insurance+"</td><td>"+r.aware+"</td><td>"+r.comments+"</td><td><button data-idx='"+i+"' class='delRow' style=\"background:#e06464;color:#fff;border:none;padding:6px;border-radius:6px\">Delete</button></td></tr>";
      });
      html+="</table><div style='margin-top:8px'><button id='deleteAll' class='danger'>Delete all responses</button></div>";
      msg.innerHTML=html;
      // attach delete handlers
      document.querySelectorAll('.delRow').forEach(btn=>btn.addEventListener('click',e=>{
        let idx=parseInt(btn.dataset.idx,10);
        if(!confirm('Delete this response?')) return;
        let arr2=loadResponses();arr2.splice(idx,1);saveResponses(arr2);document.getElementById('viewSurvey').click();
        updateDashboard(); showToast('Response deleted');
      }));
      document.getElementById('deleteAll').addEventListener('click',()=>{
        if(!confirm('Delete ALL saved responses? This cannot be undone.')) return;
        localStorage.removeItem(STORAGE_KEY);document.getElementById('viewSurvey').click();
        updateDashboard(); showToast('All responses deleted');
      });
    };

    function csvEscape(v){if(v===null||v===undefined) return '';v=(''+v).replace(/"/g,'""');return '"'+v+'"';}
    document.getElementById("exportCsv").onclick=()=>{
      let arr=loadResponses();if(!arr.length){alert("No data");return;}
      let anon=document.getElementById('exportAnon').checked;
      let header=['Time','Name','Age','Gender','Disease','Insurance','Aware','Comments'];
      let rows=[header.map(csvEscape).join(',')];
      arr.forEach(r=>{
        let name=anon?'' : r.name;
        let row=[r.time,name,r.age,r.gender,r.disease,r.insurance,r.aware,r.comments].map(csvEscape).join(',');
        rows.push(row);
      });
      let csv='\uFEFF'+rows.join('\n'); // add BOM for Excel
      let blob=new Blob([csv],{type:'text/csv;charset=utf-8;'});
      let url=URL.createObjectURL(blob);
      let a=document.createElement('a');a.href=url;a.download='survey-'+(new Date().toISOString().replace(/[:.]/g,'-'))+'.csv';a.click();URL.revokeObjectURL(url);
        showToast('CSV exported');
    };

    document.getElementById("clearForm").onclick=()=>{
      if(!confirm('Clear the form inputs?')) return;
      ["name","age","gender","disease","insurance","aware","comments"].forEach(id=>document.getElementById(id).value="");
      document.getElementById("consent").checked=false;
      document.getElementById("surveyMsg").style.display="none";
    };

    // --- Dashboard charts (Home) ---
    function drawPie(canvasId, data, colors){
      const c=document.getElementById(canvasId); if(!c) return; const ctx=c.getContext('2d');
      const total=data.reduce((s,i)=>s+i,0); let start= -0.5*Math.PI; ctx.clearRect(0,0,c.width,c.height);
      const cx=c.width/2, cy=c.height/2, r=Math.min(cx,cy)-10;
      // store slices for interaction
      c._slices=[];
      data.forEach((v,i)=>{
        const slice=(v/total)*(Math.PI*2); ctx.beginPath(); ctx.moveTo(cx,cy); ctx.fillStyle=colors[i%colors.length]; ctx.arc(cx,cy,r,start,start+slice); ctx.closePath(); ctx.fill();
        c._slices.push({start, end:start+slice, value:v, color:colors[i%colors.length], label:i});
        start+=slice;
      });
      // attach handlers
      c.onmousemove=(e)=>{
        const rect=c.getBoundingClientRect(); const x=e.clientX-rect.left; const y=e.clientY-rect.top; const dx=x-cx; const dy=y-cy; const dist=Math.sqrt(dx*dx+dy*dy);
        if(dist>r){ tooltip.style.display='none'; return; }
        let ang=Math.atan2(dy,dx); if(ang< -0.5*Math.PI) ang+=2*Math.PI; // normalize
        let found=c._slices.find(s=>ang>=s.start && ang<=s.end);
        if(found){ tooltip.style.display='block'; tooltip.style.left=(e.pageX+12)+'px'; tooltip.style.top=(e.pageY+12)+'px'; tooltip.innerHTML=(found.label)+' — '+found.value+'%'; }
        else tooltip.style.display='none';
      };
      c.onclick=(e)=>{ // click to show details
        const rect=c.getBoundingClientRect(); const x=e.clientX-rect.left; const y=e.clientY-rect.top; const dx=x-cx; const dy=y-cy; const dist=Math.sqrt(dx*dx+dy*dy);
        if(dist>r) return; let ang=Math.atan2(dy,dx); if(ang< -0.5*Math.PI) ang+=2*Math.PI; let found=c._slices.find(s=>ang>=s.start && ang<=s.end);
        if(found){ showToast('Slice: '+found.value+'%'); }
      };
      c.onmouseleave=()=>{tooltip.style.display='none'};
      return total;
    }

    function updateDashboard(){
      const sample={
        prevalencePct:28, // percent of adults with chronic disease (sample)
        distribution:{Diabetes:35,Hypertension:30,Heart:18,COPD:9,CKD:8},
        awarePct:62
      };
      let arr=loadResponses();
      let prevalence=sample.prevalencePct, distribution=sample.distribution, aware=sample.awarePct;
      // if we have survey data, compute simple local metrics
      if(arr && arr.length){
        document.getElementById('kpi-resp').textContent=arr.length;
        // compute distribution from disease field
        let counts={}; let awareCount=0, affected=0;
        arr.forEach(r=>{if(r.disease && r.disease!=='None'){counts[r.disease]=(counts[r.disease]||0)+1;affected++; if(r.name) awareCount++;}}
        );
        if(affected>0){distribution={}; Object.keys(counts).forEach(k=>distribution[k]=Math.round((counts[k]/affected)*100)); prevalence=Math.round((affected/arr.length)*100); aware=Math.round((awareCount/affected)*100);} else {document.getElementById('kpi-resp').textContent=arr.length}
      }
      // set KPIs
      document.getElementById('kpi-prevalence').textContent=prevalence+'%';
      let top=Object.entries(distribution).sort((a,b)=>b[1]-a[1])[0]; document.getElementById('kpi-top').textContent=top?top[0]: 'N/A';
      document.getElementById('kpi-aware').textContent=(aware||0)+'%';

      // draw disease pie
      const keys=Object.keys(distribution); const vals=keys.map(k=>distribution[k]); const colors=['#2a9df4','#1c6db3','#2bb673','#f4a261','#e06464','#9b59b6'];
      drawPie('chartDiseases', vals.length?vals:[1], colors);
      // legend
      const leg=document.getElementById('legendDiseases'); leg.innerHTML=''; keys.forEach((k,i)=>{let span=document.createElement('div');span.style.display='inline-block';span.style.marginRight='10px';span.innerHTML='<span style="display:inline-block;width:12px;height:12px;background:'+colors[i%colors.length]+';margin-right:6px;border-radius:3px"></span>'+k+' ('+distribution[k]+'%)';leg.appendChild(span)});

      // awareness pie
      const awareVals=[aware,100-aware]; drawPie('chartAware', awareVals, ['#2bb673','#e6f5ff']);
      document.getElementById('legendAware').innerHTML='<div style="display:inline-block;margin-right:12px"><span style="display:inline-block;width:12px;height:12px;background:#2bb673;margin-right:6px;border-radius:3px"></span>Aware ('+aware+'%)</div><div style="display:inline-block"><span style="display:inline-block;width:12px;height:12px;background:#e6f5ff;margin-right:6px;border-radius:3px"></span>Not aware ('+(100-aware)+'%)</div>';
    }

    // run dashboard update once page loads
    updateDashboard();
  </script>
</body>
</html>
