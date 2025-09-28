---
layout: default
title: MoE Mechanisms via MUI
---

<section class="hero" id="paper">
  <div class="container hero-inner">
    <div>
      <h1>
  Beyond Benchmarks: Understanding MoE Models Through
  <span style="color: var(--accent); font-weight: 700; font-size: inherit;">Internal Mechanisms</span></h1>
      <p class="lead">We study how Mixture‑of‑Experts (MoE) models work on the inside — not just how well they score. By explicitly incorporating routing signals and analyzing expert‑level behavior, our internal metric <strong>MUI</strong> exposes capacity, dynamics, and specialization beyond what benchmarks show.</p>
      <div class="badges">
        <span class="badge">MoE</span>
        <span class="badge">Evalution</span>
        <span class="badge">Neuron Activation </span>
        <span class="badge">Expert Specialization</span>
      </div>
      <div class="cta">
        <a class="button" href="" title="Paper PDF (replace link)">📄 Paper (PDF)</a>
        <a class="button secondary" href="https://github.com/" title="Code (replace link)">💻 Code (coming soon)</a>
      </div>
      <p class="meta" style="margin-top:10px;">
        Authors: 
        <a href="https://yingjiahao14.github.io/" target="_blank">Jiahao Ying</a>, 
        <a href="https://lmbxmu.github.io/" target="_blank">Mingbao Lin</a>, 
        <a href="https://faculty.smu.edu.sg/profile/sun-qianru-551" target="_blank">Qianru Sun</a>
        <a href="https://taominer.github.io/" target="_blank">Yixin Cao</a>
        · {{ site.time | date: "%Y" }}
      </p>
    </div>
    <div class="mock-card">
      <p class="meta">Abstract</p>
      <p>Mixture-of-Experts (MoE) architectures have emerged as a promising direction, offering efficiency and scalability by activating only a subset of parameters during inference. However, current research remains largely performance-centric, with limited understanding of its internal mechanisms, thereby constraining broader progress. In this work, we use an internal metric to investigate the mechanisms of MoE architecture by explicitly incorporating routing mechanisms and analyzing expert-level behaviors. Through systematic analyses of a wide range of publicly available MoE models, we uncover several findings: (interal indicator; dynamic training trajectory; collaborative experts; neuron-level patterns as proxy for data diversity). Together, these results demonstrate the potential of MUI as a complementary indicator to benchmark performance, offering new insights into the capacity, dynamics, and specialization of MoE models.</p>
    </div>
  </div>
</section>

<section class="section" id="findings">
  <div class="container">
    <h2>Key Findings</h2>
    <p class="sub">What MUI reveals across a wide range of public MoE models.</p>
    <div class="cards">
      <div class="card">
        <h3>1) Neuron utilization ↓ with model evolution</h3>
        <p>As models scale and mature, we observe reduced neuron utilization - an indicator of stronger generalization and more efficient representations.</p>
      </div>
      <div class="card">
        <h3>2) Training is dynamic benchmarks alone mislead</h3>
        <p>Benchmark scores can stay flat while MUI shows meaningful internal changes, capturing shifts in learining stages.</p>
      </div>
      <div class="card">
        <h3>3) Tasks are collaborative across experts</h3>
        <p>Successful completion typically involves multiple experts. Shared experts emerge as anchors, driving concentration and reuse.</p>
      </div>
      <div class="card">
        <h3>4) Neuron patterns ↔ data diversity</h3>
        <p>Fine‑grained activation patterns correlate with the diversity of data seen, offering a useful proxy when explicit labels are unavailable.</p>
      </div>
      <div class="card full">
        <blockquote>
          <strong>Takeaway:</strong> <em>MUI complements benchmarks.</em> It offers a richer view of capacity, dynamics, and expert specialization - informing model design and evaluation.
        </blockquote>
      </div>
    </div>
  </div>
</section>

<section class="section" id="mui">
  <div class="container">
    <h2><span style="color: var(--accent)">MUI</span> - Model Level Indicators</h2>
    <br>
     <span class="sub"><b>What is <span style="color: var(--accent)">MUI</span></b>? An internal diagnosis metric that reflects the easures the proportion of neurons required for task completion </span>
       <p>
        $$
        \textbf{MUI}_{\text{}}(\mathcal{T})=
        \frac{\left|\bigcup N_\text{activated}(s_i)\right|}
        {N \times L \times \bigl(|{E}_{s}| + |{E}_{r}|\bigr)},
        \quad  $$</p>
        where $N$ is the number of neurons per expert, $L$ is the number of MoE layers, $|{E}_{s}|$ is the number of shared experts, $|{E}_{r}|$ is the number of routed experts per layer and $N_\text{activated}(s_i)$ denotes the set of key neurons in the model that are required to process sample $s_i$ in Task $\mathcal{T}$. By comparing earlier and later versions within the same model families, we examine how MUI reflects the impact of model iteration or evolution. It indicated that later-released models consistentlyachieve stronger performance on the same datasets while exhibiting lower MUI. These newer models indeed possess higher true capability and stronger generalization,  and <span style="color: var(--accent)">MUI</span> may serve as an indicator of intrinsic capacity and generalization rather than benchmark-specific performance.
    <br>
    <div class="mui-box">
    <div class="mui-box-title">MUI as an Indicator</div>
    <div class="mui-box-content">
      Combining performance with MUI offers an indicator of a model’s underlying generalization capability,
      mitigating the risks of misleading evaluations caused by leakage.
    </div>
    </div>
    <br>
    <p> MUI and Performance. Click to focus within the different model families </p> 
        <div class="container">
        <div class="legend-actions">
          <button data-group="DeepSeek-Light" class="legend-chip on">DeepSeek-Light</button>
          <button data-group="DeepSeek" class="legend-chip on">DeepSeek</button>
          <button data-group="Qwen" class="legend-chip on">Qwen</button>
          <button data-group="GPT-OSS" class="legend-chip on">GPT-OSS</button>
        </div>
        <div class="chart-box">
          <canvas id="muiScatter" aria-label="MUI vs Performance" role="img"></canvas>
        </div>
      </div>
      </div>
    <!-- <img src="{{ '/assets/figures/main2.png' | relative_url }}" class="zoomable figure" alt="MoE illustration"> -->
    <!-- <canvas id="muiBar" height="200" aria-label="Key experts ratio by model" role="img"></canvas> -->
    <!-- <div class="cards">
      <div class="card">
        <h3>Why another metric?</h3>
        <ul class="list">
          <li>Benchmarks show <em>what</em> but not <em>how</em>.</li>
          <li>Routing/expert signals contain rich inductive-bias information.</li>
          <li>Helps compare models with similar scores but different mechanisms.</li>
        </ul>
      </div>
      <div class="card">
        <h3>Signals considered</h3>
        <ul class="list">
          <li>Per-token routing probabilities and selected experts.</li>
          <li>Expert-level activation sparsity and overlap.</li>
          <li>Neuron-level activation statistics within experts.</li>
        </ul>
      </div>
      <div class="card">
        <h3>Practical uses</h3>
        <ul class="list">
          <li>Track training dynamics beyond loss curves.</li>
          <li>Diagnose specialization &amp; collapse.</li>
          <li>Estimate data diversity via fine-grained activations.</li>
        </ul>
      </div>
      <div class="card">
        <h3>Limitations</h3>
        <ul class="list">
          <li>Requires internal access (hooks/telemetry).</li>
          <li>Not a drop-in replacement for benchmarks.</li>
          <li>Interpretation depends on model &amp; training recipe.</li>
        </ul>
      </div>
    </div> -->
    <br>
    <br>
    <div class="container">
    <h2>Training Trajectories</h2>
    Does MUI decrease monotonically throughout training, or do different phases exhibit distinct trajectories? To address this, we monitor MUI for OLMoE serise models across the entire training process, with the goal of deriving insights that can inform training strategies and model development.  At earlier stages, performance improvements are accompanied by an increase in MUI, which we refer to as the <span style="color:#4F95D9;font-weight:700">Accumulating</span>. At later stages, however, further performance gains occur together with a decrease in MUI, which we call the <span style="color:#10a37f;font-weight:700">Evolving</span>.
      <br>
      <br>
    <div class="chart-row">
      <div class="chart-box sm">
        <canvas id="olmoeOverall" aria-label="OLMoE overall trajectory" role="img"></canvas>
      </div>
      <div class="chart-box sm">
        <canvas id="olmoeGSM8K" aria-label="OLMoE GSM8K trajectory" role="img"></canvas>
      </div>
    </div>
    <div class="mui-box">
    <div class="mui-box-title">MUI Moniting MoE Training</div>
    <div class="mui-box-content">
     Monitoring performance alone is insufficient; MUI provides a complementary perspective for performance for detecting divergent trajectories and adjusting training accordingly. 
    For example, as shown above, in coding tasks such as MBPP, OLMoE consistently remains in the Accumulating phase without entering the Evolving phase. This suggests that additional coding data, or a higher proportion of coding tasks during earlier training stages, may be required to help the model further improve its generalization ability. 
    </div>
    </div>
  </div>
    <br>
    <br>
  <div class="container">
    <h2>Collaborative Expert Contributions</h2>
    We here extend our analysis to the expert level by calculating the Task specific key Experts:
    <p>
    $$ 
    \text{KeyExpertProportion} (\mathcal{T})=\frac{ |  E_{\text{key}}(\mathcal{T}) | }{ L \times (|{E}_{s}| + |{E}_{r}|) }, 
    $$ where  $E_{\text{key}}(\mathcal{T})$ is the experts that consistently contribute across taske $\mathcal{T}$. We find that, MoE models, activating a larger number of experts while requiring fewer neurons within each expert is often associated with stronger true capability and better generalization. With GPT-OSS have the highest proportion of key experts among the models studied.
    </p>
      <br>
      <br>
    <div class="chart-box sm">
      <canvas id="keyExpertBar" aria-label="Key Expert Proportion (Math)" role="img"></canvas>
    </div>
  </div>
      <br>
      <br>
  <div class="container">
  After analyzing the overall trend of expert utilization, we further analyze the distribution of key experts, particularly in light of architectural differences between shared and routed experts. Here we depict the <strong>top-10 Experts for Task MMLU</strong>. For MoE architectures that include shared experts, the findings reveal that the top-10 most frequently activated experts are exclusively shared experts. By contrast, in GPT-OSS, a routed-only MoE, the activation rate is extremely low.
   <br>
    <br>
  <div class="chart-row two">
    <div class="chart-box sm">
      <canvas id="topExpertsQwen"></canvas>
    </div>
    <div class="chart-box sm">
      <canvas id="topExpertsGPT"></canvas>
    </div>
  </div>
   <div class="mui-box">
    <div class="mui-box-title">Expert "Collaboration" in MoE</div>
    <div class="mui-box-content">
     Although the feed-forward networks in MoE architectures are referred to as "Experts,"
it is difficult in practice to interpret them as independent task-specific units. In models having shared experts, their persistent activation leads to concentrated responsibility within the shared pool, whereas in routed-only architectures, the influence of load-balancing losses drives a more dispersed "many-hands" collaboration among a broader set of experts. 
    </div>
    </div>
</div>
   <!-- <br>
    <br>
<div class="container">
 <h2>Data measurement</h2>
  Activation patterns can be leveraged as an internal proxy for measuring the diversity of input data.  Neuron-level MUI offers finer granularity and efficiency.
</div> -->


</section>


<div id="img-modal" class="modal" aria-hidden="true">
  <span class="modal-close" aria-label="Close">&times;</span>
  <img id="img-modal-content" class="modal-content" alt="">
</div>

<section class="section" id="resources">
  <div class="container">
    <h2>Resources</h2>
    <p class="sub">Replace links below with your artifacts.</p>
    <div class="cards">
      <div class="card">
        <h3>Paper</h3>
        <p><a href="#" title="Replace with your arXiv/URL">📄 arXiv / PDF link</a></p>
      </div>
      <div class="card">
        <h3>Code</h3>
        <p><a href="#" title="https://github.com/ALEX-nlp/MUI-EvalL">💻 GitHub Repository</a></p>
      </div>
      <div class="card">
        <h3>BibTeX</h3>
        <pre><code>@inproceedings{{mui-moe,
  title={{Understanding MoE Mechanisms via an Internal Metric (MUI)}},
  author={{Your Name and Coauthors}},
  year={{2025}},
  url={{https://example.com/paper}}}
}</code></pre>
      </div>
      <div class="card">
        <h3>Contact</h3>
        <p><a href="jhying.2022@phdcs.smu.edu.sg">📧 jhying.2022@phdcs.smu.edu.sg</a></p>
       <p><a href="caoyixin2011@gmail.com">📧 caoyixin2011@gmail.com</a></p>
      </div>
    </div>
  </div>
</section>
