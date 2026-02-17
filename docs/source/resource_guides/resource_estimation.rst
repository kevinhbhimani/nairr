===============================
Generalized Resource Estimation
===============================

.. raw:: html

Overview
--------
This guide is intended for new researchers interested in submitting a NAIRR Pilot proposal who have little experience with HPC or large-scale resources. This guide will help researchers complete the resource estimation section while submitting a NAIRR Pilot proposal.

Learning Outcomes
-----------------
* Translate a research compute needs into CPU-hours, GPU-hours, node-hours, RAM, and storage.
* Produce an estimate for scaling code on High Performance Computing Systems.


Reference links
---------------
Information about currently available resources for **researchers** is at
`NAIRR Pilot: Resource Requests <https://nairrpilot.org/opportunities/allocations>`_,
and for **educators** at
`NAIRR Pilot: Education Call <https://nairrpilot.org/opportunities/education-call>`_.
A step by step request walkthrough is available on YouTube:
`How to request resources <https://www.youtube.com/watch?v=GCTv5OjI1ys&t=184s>`_
with slides linked in the video description.

Getting Started
---------------
1. **Define the scenarios to run**
  List the concrete workloads such as preprocessing, training, evaluation, inference, and post processing. For each workload, note expected run count, inputs and outputs, and per run resource needs.

2. **Run a small pilot**
  Execute the same code path on a reduced problem that completes quickly. Record wall time, peak GPU and CPU memory, and output volume such as checkpoints and logs. Keep these measurements for citation in the proposal.

3. **Measure throughput and scaling**
  Track a stable throughput metric such as tokens per second, images per second, steps per second, or records per second. Scale from pilot to full runs by dividing total work by throughput and converting to hours. If possible, run at two scales such as 1 GPU and 2 GPUs and report observed efficiency.

4. **Decide concurrency**
  Choose a realistic number of concurrent jobs based on queue limits and workflow dependencies. Concurrency affects calendar time, not total GPU hours or CPU hours. Note any sequential stages such as preprocessing before training.

5. **Convert to allocation units**
  Compute GPU hours as runs times hours per run times GPUs per run, and CPU core hours as runs times hours per run times cores per run. Use node hours when allocation policy is node based or when memory per node is the constraint.

6. **Add overhead**
  Add a buffer for retries, debugging, profiling, and extra evaluation, often 20 to 30 percent early in a project. If overhead is large, break it into buckets such as profiling runs times runtime times resources. Provide a brief justification for the chosen buffer.

7. **Map to SUs and summarize**
  Convert totals to service units using site specific SU per GPU hour and SU per core hour factors. Report raw totals and SU totals, plus a rough calendar time estimate based on concurrency. Detail the storage needs, separating persistent project storage, peak scratch, and any archive.

Unit conversions and formulas
-----------------------------
Definitions for metrics in the guide:

- **GPU hours** = wall hours × GPUs per job × number of jobs
- **CPU core hours** = wall hours × CPU cores per job × number of jobs
- **Node hours** = wall hours × nodes per job × number of jobs
- **Memory usage** can be reported as peak GB per job and total GB hours if needed
- **Storage** is typically reported as average TB retained per month plus peak scratch needs


Storage
-----------------------
Plan for the storage classes that will be used and how data flows between different storages:

- **Project storage** (persistent, shared, moderate speed)  
  Long-lived space for datasets, checkpoints, and logs. Backed up and quota-limited.

- **Scratch** (ephemeral, very fast, local)  
  Temporary high-performance space used during runs. Purged automatically and not for long term storage. A common retention window is **~7–30 days**, but policies vary by host site.

- **Archive / long-term storage** (persistent, slower, cost-efficient)  
  For the data that rarely accessed

  .. note::
   Scratch is typically **not backed up** and is often purged on a schedule. Plan to copy important data and outputs to project storage regularly.


Interactive Estimator
---------------------

The SUs scale quickly. To get an estimate for the SU requirement, consider using the following widget.

.. raw:: html

   <div id="nairr-widget" style="font:14px/1.4 system-ui, -apple-system, Segoe UI, Roboto, sans-serif; border:1px solid #e5e7eb; border-radius:12px; padding:16px; max-width:900px;">
     <style>
       #nairr-widget .row{display:grid;grid-template-columns:220px 1fr 90px;gap:10px;align-items:center;margin:10px 0;}
       #nairr-widget input[type=range]{width:100%;}
       #nairr-widget .small{color:#6b7280;font-size:12px}
       #nairr-widget .num{width:80px}
       #nairr-widget .card{display:grid;grid-template-columns:1fr 1fr 1fr;gap:12px;margin-top:12px}
       #nairr-widget .box{border:1px solid #e5e7eb;border-radius:10px;padding:10px}
       #nairr-widget h4{margin:12px 0 6px 0;font-size:14px}
       #nairr-widget .big{font-weight:600;font-size:18px}
       #nairr-widget code{background:#f8fafc;padding:0 4px;border-radius:4px}
     </style>

     <div class="row">
       <label><b>Number of runs</b></label>
       <input id="runs" type="range" min="1" max="10000" value="500" oninput="W.upd()">
       <input id="runs_n" class="num" type="number" min="1" max="500" value="1000" oninput="W.sync('runs')">
     </div>

     <div class="row">
       <label><b>Hours per run</b></label>
       <input id="hours" type="range" min="0.1" max="240" step="0.1" value="10" oninput="W.upd()">
       <input id="hours_n" class="num" type="number" min="0.1" step="0.1" value="10" oninput="W.sync('hours')">
     </div>

     <div class="row">
       <label><b>CPU cores per run</b></label>
       <input id="cores" type="range" min="1" max="2048" value="8" oninput="W.upd()">
       <input id="cores_n" class="num" type="number" min="1" max="2048" value="8" oninput="W.sync('cores')">
     </div>

     <div class="row">
       <label><b>GPUs per run</b></label>
       <input id="gpus" type="range" min="0" max="256" value="1" oninput="W.upd()">
       <input id="gpus_n" class="num" type="number" min="0" max="256" value="1" oninput="W.sync('gpus')">
     </div>

     <div class="row">
       <label><b>Overhead (%)</b> <span class="small"></span></label>
       <input id="buffer" type="range" min="0" max="100" value="20" oninput="W.upd()">
       <input id="buffer_n" class="num" type="number" min="0" max="100" value="20" oninput="W.sync('buffer')">
     </div>

     <div class="row">
       <label><b>Concurrent jobs </b><span class="small">(only used for calendar time)</span></label>
       <input id="conc" type="range" min="1" max="256" value="10" oninput="W.upd()">
       <input id="conc_n" class="num" type="number" min="1" max="256" value="10" oninput="W.sync('conc')">
     </div>

     <div class="row">
       <label><b>SU per <code>core-hour</code> </b><span class="small">(based on host site policy)</span></label>
       <input id="su_core" type="range" min="0" max="10" step="0.1" value="1" oninput="W.upd()">
       <input id="su_core_n" class="num" type="number" step="0.1" value="1" oninput="W.sync('su_core')">
     </div>

     <div class="row">
       <label><b>SU per <code>GPU-hour</code> </b><span class="small"></span></label>
       <input id="su_gpu" type="range" min="0" max="200" step="1" value="32" oninput="W.upd()">
       <input id="su_gpu_n" class="num" type="number" step="1" value="32" oninput="W.sync('su_gpu')">
     </div>

     <div class="card">
       <div class="box">
         <h4>CPU total</h4>
         <div class="big" id="cpu_hours">—</div>
         <div class="small">core-hours = runs × hours/run × cores/run × (1 + overhead)</div>
       </div>
       <div class="box">
         <h4>GPU total</h4>
         <div class="big" id="gpu_hours">—</div>
         <div class="small">GPU-hours = runs × hours/run × GPUs/run × (1 + overhead)</div>
       </div>
       <div class="box">
         <h4>Calendar time (rough)</h4>
         <div class="big" id="wall_days">—</div>
         <div class="small">days ≈ (runs × hours/run) ÷ concurrent jobs ÷ 24</div>
       </div>
     </div>

     <div class="card">
       <div class="box">
         <h4>CPU SUs</h4>
         <div class="big" id="cpu_su">—</div>
         <div class="small">= core-hours × SU/core-hour</div>
       </div>
       <div class="box">
         <h4>GPU SUs</h4>
         <div class="big" id="gpu_su">—</div>
         <div class="small">= GPU-hours × SU/GPU-hour</div>
       </div>
       <div class="box">
         <h4>Total SUs</h4>
         <div class="big" id="total_su">—</div>
         <div class="small">sum of CPU and GPU SUs</div>
       </div>
     </div>

     <script>
       const W = {
         ids:['runs','hours','cores','gpus','buffer','conc','su_core','su_gpu'],
         g(i){return document.getElementById(i)},
         val(i){return parseFloat(this.g(i).value)},
         fmt(n){return (n>=1000)? n.toLocaleString(undefined,{maximumFractionDigits:0}) : n.toLocaleString(undefined,{maximumFractionDigits:2})},
         sync(id){
           // keep range <-> number in sync
           this.g(id).value = this.g(id+'_n').value;
           this.upd();
         },
         upd(){
           // keep number boxes synced from ranges
           this.ids.forEach(id=>{ this.g(id+'_n').value = this.g(id).value });
           const runs=this.val('runs');
           const hours=this.val('hours');
           const cores=this.val('cores');
           const gpus=this.val('gpus');
           const buf=(1+this.val('buffer')/100.0);
           const conc=Math.max(1,this.val('conc'));
           const su_core=this.val('su_core');
           const su_gpu=this.val('su_gpu');

           const cpu_hours = runs * hours * cores * buf;
           const gpu_hours = runs * hours * gpus * buf;

           const wall_days = (runs * hours) / conc / 24.0;

           const cpu_su = cpu_hours * su_core;
           const gpu_su = gpu_hours * su_gpu;
           const total_su = cpu_su + gpu_su;

           this.g('cpu_hours').textContent = this.fmt(cpu_hours);
           this.g('gpu_hours').textContent = this.fmt(gpu_hours);
           this.g('wall_days').textContent = this.fmt(wall_days);
           this.g('cpu_su').textContent = this.fmt(cpu_su);
           this.g('gpu_su').textContent = this.fmt(gpu_su);
           this.g('total_su').textContent = this.fmt(total_su);
         }
       };
       W.upd();
     </script>
   </div>

.. note::
   Set **SU per core-hour** and **SU per GPU-hour** to match the resource request.

Hote Site policy
---------------- 
Be mindful of site policies and constraints. It is recommend to understand the following factors while planning computations:
* **Maximum wall time per job**
* **Maximum GPUs per job**
* **Job count limits and job array limits**
* **Per user and per project storage quotas**
* **Scratch purge policy and retention window**
* **Whether preemption is possible on the requested resource**


Overhead: what to include and how to estimate
------------------------------------------------------
Most projects need a buffer to cover work that is real, expected, and often forgotten in early estimates.
Overhead is any compute and storage consumed outside the ideal production runs.

Common sources of overhead
~~~~~~~~~~~~~~~~~~~~~~~~~~
- **Retries and restarts** such as preemptions, node failures and network interruptions
- **Queue and workflow variability** in case of failed jobs due to walltime limits and scheduler constraints
- **Profiling and performance tuning** profiling runs can add up
- **Hyperparameter exploration** even a small grid search can add to total compute cost
- **Data validation and integrity checks** processing data for modelling and inference is commonly underestimated
- **Unit/integration tests for custom code** especially if tests are non-trivial or run frequently
- **Rebuild cycles** some large codebase build times can also add to the overall compute

A practical way to estimate overhead
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Use one of these approaches are:

1) **Rule-of-thumb buffer:**
   Add **20–30%** if the project is in early in development or new to HPC workflows.

2) **Component-based overhead:**
   Estimate overhead as the sum of a few explicit buckets, e.g.:

   - tests: [X test runs] × [test runtime] × [resources requested]
   - profiling: [Y profiling runs] × [runtime] × [resources]
   - retries: [Z%] of production runtime
   - hyperparameter search: [N extra runs] × [runtime] × [resources]

3) **Historical rate:**
   If past runs are avialbel, they can be use it to estimate an “overhead factor”:

.. note::
   Unit tests and build-debug loops can meaningfully impact allocations, especially when tests fail and software must be rebuilt or reconfigured. If tests run on every build or before every large run, it is recommended to include them in the overhead estimate.

Recommended Reading
-------------------
The pages below provides a brief guide to estimate resources for different architectures.

* :doc:`CPU Estimate <cpu_estimation>`
* :doc:`GPU Estimate <gpu_estimation>`
