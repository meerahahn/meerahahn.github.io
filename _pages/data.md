---
layout: default
urltitle:  "Data · VLN-CE"
title: "Data · VLN-CE"
permalink: /data
---

<div class="row" style="margin-top:30px;">
  <div class="col-xs-12">
    <h1>VLN-CE Dataset</h1>
  </div>
</div>

<hr>
<div class="row">
  <div class="col-xs-12">
    <p>
      The dataset used in VLN-CE is the Room-to-Room dataset by <a href="https://bringmeaspoon.org/">Anderson
      et al. 2018</a> ported from the Matterport3D Simulator to the Habitat Simulator.
    </p>
  </div>
</div>

<div class="row">
  <div class="col-xs-12">
    <h2>R2R_VLNCE_v1-2</h2>
  </div>
  <div class="col-xs-12">
    <a
      href="https://drive.google.com/file/d/1YDNWsauKel0ht7cx15_d9QnM6rS4dKUV/view?usp=sharing"
      onClick="ga('send', 'event', { eventCategory: 'download', eventAction: 'click', eventLabel: 'R2R_VLNCE_v1-2', eventValue: 0});"
    >R2R_VLNCE_v1-2.zip</a> (3 MB)
    <ul style="margin:10px 10px 10px;"  class="col-xs-12">
      <li>train: 10819 episodes, 61 scenes</li>
      <li>val_seen: 778 episodes, 53 scenes</li>
      <li>val_unseen: 1839 episodes, 11 scenes</li>
      <li>test: 3408 episodes, 18 scenes</li>
    </ul>
    <br>
    <a
      href="https://drive.google.com/file/d/18sS9c2aRu2EAL4c7FyG29LDAm2pHzeqQ/view?usp=sharing"
      onClick="ga('send', 'event', { eventCategory: 'download', eventAction: 'click', eventLabel: 'R2R_VLNCE_v1-2_preprocessed', eventValue: 0});"
    >R2R_VLNCE_v1-2_preprocessed.zip</a> (345 MB)
    <ul style="margin:10px 10px 10px;"  class="col-xs-12">
      <li>Adds an augmented split, envdrop: 146413 episodes, 60 scenes (ported from <a href="https://github.com/airsplay/R2R-EnvDrop">R2R-EnvDrop</a>)</li>
      <li>Contains <code>embeddings.json.gz</code> which is extracted from a 50d <a href="https://nlp.stanford.edu/projects/glove/">GloVe</a> file</li>
      <li>Instruction tokens are mapped to match the provided embeddings</li>
      <li><code>{split}_gt.json.gz</code> contains ground truth actions and step locations for each episode (excluding the test split)</li>
    </ul>
  </div>
  <br>
</div>

<div class="row">
  <div class="col-xs-12">
    <h3 style="margin:10px 0;">Format of <code>{split}.json.gz</code></h3>
    <pre><code>{
    'episodes' = [
        {
            'episode_id': 1,
            'trajectory_id': 4,
            'scene_id': 'mp3d/7y3sRwLe3Va/7y3sRwLe3Va.glb',
            'instruction': {
                'instruction_text': 'Go around the right side...',
                'instruction_tokens': [982, 141, 2202, ..., 0, 0, 0]
            },
            'start_position': [-16.267200469970703, 0.1518409252166748, 0.7207760214805603],
            'start_rotation': [0.0, 0.0007963267107332633, 0.0, 0.9999996829318346],
            'goals': [
                {
                    'position': [-12.337400436401367, 0.1518409252166748, 4.213699817657471],
                    'radius': 3.0
                }
            ],
            'reference_path': [
                [-16.267200469970703, 0.1518409252166748, 0.7207760214805603],
                [-16.284099578857422, 0.1518409252166748, 2.4123699665069580],
                ...
                [-13.907199859619140, 0.1518409252166748, 4.2282099723815920],
            ],
            'info': {'geodesic_distance': 6.425291538238525},
        },
        ...
    ],
    'instruction_vocab': [
        'word_list': [..., 'orchids', 'order', 'orient', ...],
        'word2idx_dict': {
            ...,
            'orchids': 1505,
            'order': 1506,
            'orient': 1507,
            ...
        },
        'itos': [..., 'orchids', 'order', 'orient', ...],
        'stoi': {
            ...,
            'orchids': 1505,
            'order': 1506,
            'orient': 1507,
            ...
        },
        'num_vocab': 2504,
        'UNK_INDEX': 1,
        'PAD_INDEX': 0,
    ]
}</code></pre>
  </div>
  <br>

  <div class="col-xs-12">
    <h3 style="margin:10px 0;">Format of <code>{split}_gt.json.gz</code></h3>
    <pre><code>{
    '1': {
        'actions': [2, 2, 2, ..., 0],
        'forward_steps': 27,
        'locations': [
            [-16.267200469970703, 0.1518409252166748, 0.7207760214805603],
            ...
            [-12.644463539123535, 0.1518409252166748, 4.2241311073303220]
        ]
    },
    ...
}</code></pre>
  </div>
</div>

<div class="row">
  <div class="col-xs-12">
    <h2>Versions</h2>
  </div>
  <div class="col-xs-12">
    <h3>R2R_VLNCE_v1-2 [latest]</h3>
  </div>
  <div class="col-xs-12">
    Links above. Adds the test split for inference. The test split does not have ground truth paths or goal locations. Test evaluations should be done on the new <a class="poplink" href="https://eval.ai/web/challenges/challenge-page/719">evaluation and leaderboard server</a>.
  </div>
  <div class="col-xs-12">
    <h3>R2R_VLNCE_v1-1</h3>
  </div>
  <div class="col-xs-12">
    Changes over R2R_VLNCE_v1 include:
    <ul style="margin:10px 10px 10px;"  class="col-xs-12">
      <li>Makes the <code>reference_path</code> field consistently include both start and goal locations.</li>
      <li>Makes all goal radii equal to 3.0m (<code>train</code> split in <code>R2R_VLNCE_v1_preprocessed</code> showed 2.0m). Unused in VLN-CE code.</li>
    </ul>
  </div>
  <div class="col-xs-12">
    Links to R2R_VLNCE_v1-1 (historical).
    <ul style="margin:10px 10px 10px;"  class="col-xs-12">
      <li><a
      href="https://drive.google.com/file/d/1r6tsahJYctvWefcyFKfsQXUA2Khj4qvR/view?usp=sharing"
      onClick="ga('send', 'event', { eventCategory: 'download', eventAction: 'click', eventLabel: 'R2R_VLNCE_v1-1', eventValue: 0});"
    >R2R_VLNCE_v1-1.zip</a></li>
      <li><a
      href="https://drive.google.com/file/d/1jNEDBiv7SnsBpXLLt7nstYpS_mg71KTV/view?usp=sharing"
      onClick="ga('send', 'event', { eventCategory: 'download', eventAction: 'click', eventLabel: 'R2R_VLNCE_v1-1_preprocessed', eventValue: 0});"
    >R2R_VLNCE_v1-1_preprocessed.zip</a></li>
    </ul>
  </div>
  <div class="col-xs-12">
    <h3>R2R_VLNCE_v1</h3>
  </div>
  <div class="col-xs-12">
    Original release of the R2R_VLNCE dataset (historical).
    <ul style="margin:10px 10px 10px;"  class="col-xs-12">
      <li><a
      href="https://drive.google.com/file/d/1k9LLJGeDGLIO2wxtWhzjGHhvQ2t2aJBQ/view?usp=sharing"
      onClick="ga('send', 'event', { eventCategory: 'download', eventAction: 'click', eventLabel: 'R2R_VLNCE_v1', eventValue: 0});"
    >R2R_VLNCE_v1.zip</a></li>
      <li><a
      href="https://drive.google.com/file/d/1IDM4eEMTJDKN6-mGTSmqSkv620hCd_TX/view?usp=sharing"
      onClick="ga('send', 'event', { eventCategory: 'download', eventAction: 'click', eventLabel: 'R2R_VLNCE_v1_preprocessed', eventValue: 0});"
    >R2R_VLNCE_v1_preprocessed.zip</a></li>
    </ul>
  </div>
  <br>
</div>