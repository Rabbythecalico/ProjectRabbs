<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>ProjectRabs — Admin Panel</title>
    <style>
      :root {
        --bg: #f5f7ff;
        --panel: #ffffff;
        --soft: #eef2ff;
        --primary: #4c6fff;
        --primary-dark: #2d4ed8;
        --green: #28b67a;
        --red: #e85d75;
        --gold: #f4c95d;
        --ink: #1e2437;
        --muted: #66708c;
        --shadow: rgba(28, 38, 59, 0.1);
      }

      * { box-sizing: border-box; }
      body {
        margin: 0;
        font-family: Arial, Helvetica, sans-serif;
        background: linear-gradient(180deg, #f8f9ff 0%, #edf3ff 100%);
        color: var(--ink);
      }

      a { color: inherit; text-decoration: none; }
      .container { max-width: 1280px; margin: 0 auto; padding: 24px 20px 60px; }

      .topbar {
        display: flex;
        justify-content: space-between;
        align-items: center;
        gap: 16px;
        background: rgba(255,255,255,0.72);
        border: 1px solid rgba(76,111,255,0.1);
        border-radius: 18px;
        padding: 16px 20px;
        backdrop-filter: blur(8px);
        box-shadow: 0 10px 24px var(--shadow);
      }

      .brand {
        display: flex;
        align-items: center;
        gap: 12px;
        font-weight: 800;
      }

      .brand-badge {
        width: 42px; height: 42px; border-radius: 50%;
        display: grid; place-items: center;
        background: linear-gradient(135deg, var(--primary), #7c5cff);
        color: white;
        box-shadow: 0 8px 18px rgba(76,111,255,0.25);
      }

      .nav {
        display: flex;
        align-items: center;
        gap: 10px;
        flex-wrap: wrap;
      }

      .nav a, .nav button {
        border: none;
        border-radius: 999px;
        padding: 10px 16px;
        background: var(--soft);
        color: var(--ink);
        font-weight: 700;
        cursor: pointer;
      }

      .nav .primary {
        background: var(--primary);
        color: white;
      }

      .hero {
        margin-top: 22px;
        background: linear-gradient(135deg, #ffffff 0%, #eef5ff 100%);
        border-radius: 28px;
        padding: 26px;
        box-shadow: 0 18px 36px var(--shadow);
      }

      .eyebrow {
        text-transform: uppercase;
        letter-spacing: 0.14em;
        font-size: 12px;
        color: var(--primary);
        font-weight: 800;
      }

      h1, h2, h3 { margin-top: 0; }
      h1 {
        font-size: clamp(2rem, 4vw, 3.1rem);
        margin: 12px 0 14px;
      }

      .hero-grid {
        display: grid;
        grid-template-columns: 1.2fr 0.8fr;
        gap: 22px;
        align-items: center;
      }

      .summary {
        color: var(--muted);
        line-height: 1.65;
        margin-bottom: 18px;
      }

      .cta-row {
        display: flex;
        flex-wrap: wrap;
        gap: 12px;
      }

      .btn {
        border: none;
        border-radius: 12px;
        padding: 12px 18px;
        font-weight: 800;
        cursor: pointer;
      }

      .btn.primary { background: var(--primary); color: white; }
      .btn.green { background: var(--green); color: white; }
      .btn.red { background: var(--red); color: white; }
      .btn.soft { background: var(--soft); color: var(--ink); }

      .mini-panel {
        background: linear-gradient(135deg, #edf1ff 0%, #f3edff 100%);
        border-radius: 22px;
        padding: 18px;
      }

      .stats {
        display: grid;
        grid-template-columns: repeat(4, minmax(0,1fr));
        gap: 14px;
        margin-top: 28px;
      }

      .stat {
        background: #fff;
        border-radius: 18px;
        padding: 18px 12px;
        box-shadow: 0 10px 18px rgba(33, 45, 77, 0.05);
        text-align: center;
      }

      .stat strong { display: block; font-size: 28px; }
      .stat span { color: var(--muted); font-size: 12px; }

      .section {
        display: grid;
        grid-template-columns: 1.2fr 0.8fr;
        gap: 22px;
        margin-top: 26px;
      }

      .panel {
        background: var(--panel);
        border-radius: 24px;
        box-shadow: 0 18px 36px var(--shadow);
        padding: 22px;
      }

      table {
        width: 100%;
        border-collapse: collapse;
      }

      th, td {
        text-align: left;
        padding: 14px 10px;
        border-bottom: 1px solid rgba(102,112,140,0.12);
        vertical-align: middle;
      }

      th {
        font-size: 12px;
        text-transform: uppercase;
        letter-spacing: 0.08em;
        color: var(--muted);
      }

      .status {
        display: inline-block;
        padding: 7px 10px;
        border-radius: 999px;
        font-size: 12px;
        font-weight: 800;
      }

      .status.pending { background: #fff3d5; color: #8a6700; }
      .status.approved { background: #e1f7eb; color: #147c52; }
      .status.flagged { background: #ffe6eb; color: #a93a4d; }

      .actions {
        display: flex;
        gap: 8px;
        flex-wrap: wrap;
      }

      .chip {
        background: var(--soft);
        border-radius: 999px;
        padding: 8px 10px;
        font-size: 12px;
        font-weight: 700;
        color: var(--ink);
      }

      @media (max-width: 980px) {
        .hero-grid, .section { grid-template-columns: 1fr; }
        .stats { grid-template-columns: repeat(2, minmax(0,1fr)); }
      }
    </style>
  </head>
  <body>
    <div class="container">
      <header class="topbar">
        <div class="brand">
          <div class="brand-badge">⚙️</div>
          <div>ProjectRabs Admin</div>
        </div>
        <nav class="nav">
          <a href="index.html">Home</a>
          <a href="user.html">User</a>
          <a href="admin.html" class="primary">Admin</a>
        </nav>
      </header>

      <section class="hero">
        <div class="hero-grid">
          <div>
            <div class="eyebrow">Moderation Center</div>
            <h1>Review and approve the community feed</h1>
            <div class="summary">
              Keep the board safe, joyful, and organized. Quickly approve new characters, flag risky entries, and monitor activity across the ProjectRabs community.
            </div>
            <div class="cta-row">
              <button class="btn primary">Review queue</button>
              <button class="btn soft">Export report</button>
            </div>
          </div>

          <div class="mini-panel">
            <h3 style="margin-bottom: 12px;">Today</h3>
            <div class="chip">34 new submissions</div>
            <div class="chip" style="margin-top: 12px;">12 flagged</div>
            <div class="chip" style="margin-top: 12px;">7 approval reminders</div>
          </div>
        </div>

        <div class="stats">
          <div class="stat">
            <strong>1,284</strong>
            <span>Total OCs</span>
          </div>
          <div class="stat">
            <strong>641</strong>
            <span>Approved</span>
          </div>
          <div class="stat">
            <strong>49</strong>
            <span>Flagged</span>
          </div>
          <div class="stat">
            <strong>94%</strong>
            <span>Response rate</span>
          </div>
        </div>
      </section>

      <section class="section">
        <div class="panel">
          <h2>Submission queue</h2>
          <table>
            <thead>
              <tr>
                <th>Creator</th>
                <th>Character</th>
                <th>Theme</th>
                <th>Status</th>
                <th>Action</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td>Rabby</td>
                <td>Violet Frost</td>
                <td>Moonlit magic</td>
                <td><span class="status pending">Pending</span></td>
                <td>
                  <div class="actions">
                    <button class="btn green">Approve</button>
                    <button class="btn red">Flag</button>
                  </div>
                </td>
              </tr>
              <tr>
                <td>Nia</td>
                <td>Luna Bloom</td>
                <td>Garden dream</td>
                <td><span class="status approved">Approved</span></td>
                <td>
                  <div class="actions">
                    <button class="btn soft">Review</button>
                  </div>
                </td>
              </tr>
              <tr>
                <td>Elle</td>
                <td>Driftling</td>
                <td>Space glitch</td>
                <td><span class="status flagged">Flagged</span></td>
                <td>
                  <div class="actions">
                    <button class="btn green">Resolve</button>
                    <button class="btn soft">Notes</button>
                  </div>
                </td>
              </tr>
            </tbody>
          </table>
        </div>

        <div class="panel">
          <h2>Quick notes</h2>
          <div class="chip" style="display:block; width: fit-content;">Moderation policy updated</div>
          <div class="chip" style="display:block; width: fit-content; margin-top: 12px;">3 content warnings active</div>
          <div class="chip" style="display:block; width: fit-content; margin-top: 12px;">Weekly digest ready</div>

          <div style="margin-top: 22px; background: #f7f9ff; border-radius: 16px; padding: 16px; color: var(--muted); line-height: 1.6;">
            Admin summary: the community remains healthy. The highest volume is in fantasy and pastel-themed OC design.
          </div>
        </div>
      </section>
    </div>
  </body>
</html>
