---
layout: default
title: "Taxonomy of edge blockchain network designs"
description: "A taxonomy of 12 edge blockchain network designs and an availability analysis against five failure scenarios."
---

<section class="hero">
  <div class="hero-inner">
    <p class="venue-badge">
      <span class="venue-name">European Conference on Software Architecture (ECSA)</span>
      <span class="venue-sep">·</span>
      <span>Springer LNCS</span>
      <span class="venue-sep">·</span>
      <span>pp. 172–180</span>
      <span class="venue-sep">·</span>
      <span>2021</span>
    </p>

    <h1 class="paper-title">Taxonomy of edge blockchain network designs</h1>
    <p class="paper-subtitle">A classification of network designs for blockchains operating at the network's edge.</p>

    <p class="authors">
      <span><strong>Nguyen Khoi Tran</strong><sup>1</sup></span>
      <span class="dot">·</span>
      <span><strong>M. Ali Babar</strong><sup>1</sup></span>
    </p>

    <p class="affiliations">
      <sup>1</sup> The University of Adelaide, South Australia, Australia
    </p>

    <div class="hero-actions">
      <a class="btn btn-primary" href="{{ '/assets/pdf/main.pdf' | relative_url }}">⬇ Download PDF</a>
      <a class="btn btn-ghost" href="https://doi.org/10.1007/978-3-030-86044-8_12" rel="noopener">View on Springer ↗</a>
    </div>
  </div>
</section>

<section class="section section--alt">
  <div class="container">
    <h2>TL;DR</h2>
    <p>
      Blockchains deployed at the network's edge (to support autonomous vehicles, edge computing, and other
      resource-constrained use cases) need <em>purpose-built</em> network designs rather than copies of
      public-chain architectures. We extracted design decisions from edge-blockchain prototypes in the literature
      and organised them into <strong>12 edge blockchain network designs</strong> grouped under single-channel
      (in-cluster, cross-cluster) and multi-channel (<em>1+n</em>, <em>1+1+n</em>) structures. We then
      evaluated each design's availability against five failure scenarios, namely losing edge devices, fog nodes,
      cloud nodes, local networks, or cross-cluster networks, across read, write, and update availability.
      The takeaway: pushing blockchain clients toward the edge maximises read availability, but resource
      constraints force a trade-off with protocol choice and write availability.
    </p>
  </div>
</section>

<section class="section">
  <div class="container">
    <h2>At a glance</h2>
    <div class="stat-grid">
      <div class="stat">
        <div class="stat-value">12</div>
        <div class="stat-label">edge blockchain network designs</div>
      </div>
      <div class="stat">
        <div class="stat-value">4</div>
        <div class="stat-label">design groups (in-cluster, cross-cluster, 1+n, 1+1+n)</div>
      </div>
      <div class="stat">
        <div class="stat-value">5</div>
        <div class="stat-label">failure scenarios evaluated</div>
      </div>
      <div class="stat">
        <div class="stat-value">3</div>
        <div class="stat-label">availability dimensions (read, write, update)</div>
      </div>
    </div>
  </div>
</section>

<section class="section section--alt">
  <div class="container">
    <h2>How we built the taxonomy</h2>
    <p>
      We built the taxonomy in three steps. First, we identified edge-blockchain prototypes from the dataset of
      an existing systematic literature review on blockchain-IoT integration, combined with top Google Scholar
      results on <em>blockchain</em> and <em>edge computing</em>. Second, we extracted design decisions from
      each selected paper using an established blockchain network design space (covering 19 dimensions and 51
      choices), splitting the decisions into <strong>protocol decisions</strong> (choice and configuration of
      the consensus protocol) and <strong>topological decisions</strong> (shape, full nodes, mining nodes,
      lightweight nodes, network interfaces, remote nodes). Third, we clustered recurring co-occurring decisions
      into the 12 designs that form the taxonomy.
    </p>
    <p>
      To make the deployment descriptions comparable across very different prototypes, we introduced a
      <em>reference edge infrastructure</em>: clusters of edge devices led by a small number of fog nodes,
      with fog nodes connecting clusters to each other and to the cloud. No edge device communicates
      directly with anything outside its cluster.
    </p>
    <figure class="figure">
      <img src="{{ '/assets/figures/reference_infrastructure.png' | relative_url }}" alt="The reference edge infrastructure used to normalise deployment descriptions across the evaluated prototypes">
      <figcaption>
        The reference edge infrastructure: clusters of edge devices led by fog nodes, with fog nodes connecting clusters to each other and to the cloud.
      </figcaption>
    </figure>
  </div>
</section>

<section class="section">
  <div class="container">
    <h2>The taxonomy</h2>
    <p>
      Despite the diversity of options, the existing edge-blockchain prototypes converged on a few designs.
      We organised them hierarchically. The top-level split is by the number of blockchain channels in the
      edge infrastructure.
    </p>

    <ul class="design-tree">
      <li>
        <strong>Single-channel designs</strong>: one channel across the whole edge infrastructure, or several independent channels that don't talk to each other.
        <ul>
          <li><strong>In-cluster</strong>: channel is bounded by a device cluster. Full and mining nodes are either on edge devices (PoA only) or offloaded to fog nodes.</li>
          <li><strong>Cross-cluster</strong>: channel spans multiple clusters. Common patterns are blockchain on fog nodes only, or full and mining nodes on both fog and edge (PoA only).</li>
        </ul>
      </li>
      <li>
        <strong>Multi-channel designs</strong>: multiple channels covering different sets of hardware nodes.
        <ul>
          <li><strong>1+n</strong>: n in-cluster channels plus one cross-cluster channel (typically hosted by fog nodes or cloud servers).</li>
          <li><strong>1+1+n</strong>: adds a third tier, namely a cloud-level channel, a fog-level cross-cluster channel, and n in-cluster channels.</li>
        </ul>
      </li>
    </ul>

    <figure class="figure">
      <img src="{{ '/assets/figures/design_taxonomy.png' | relative_url }}" alt="The full taxonomy of edge blockchain network designs, classified by channel structure, node placement, and consensus protocol">
      <figcaption>
        The taxonomy: 12 edge blockchain network designs classified by structure, node placement, and consensus protocol (PoW or PoA).
      </figcaption>
    </figure>
  </div>
</section>

<section class="section section--alt">
  <div class="container">
    <h2>Availability findings</h2>
    <p>
      We evaluated each design's availability from the perspective of an edge device (a robot, an autonomous
      vehicle) along three dimensions: <em>read</em> (can it read blockchain state?), <em>write</em> (can it commit
      new transactions?), and <em>update</em> (will those updates reach other devices, locally or globally?).
      We tested the designs against five failure scenarios: losing <em>n/3</em> of edge devices in a local
      cluster, a local fog node, a cloud node, the local edge network, or the cross-cluster network.
    </p>

    <div class="finding">
      <h3>Read availability: pushing clients to the edge wins</h3>
      <div class="finding-grid">
        <div class="finding-item"><span class="num">100%</span><span class="lbl">of failures tolerated by designs placing clients on edge devices</span></div>
        <div class="finding-item"><span class="num">66.7%</span><span class="lbl">of designs disrupted by losing a fog node or in-cluster network</span></div>
        <div class="finding-item"><span class="num">0%</span><span class="lbl">read availability for cloud-only designs on any cloud disconnect</span></div>
      </div>
    </div>

    <div class="finding">
      <h3>Write and update availability: PoW beats PoA when networks fragment</h3>
      <figure class="figure figure--small">
        <img src="{{ '/assets/figures/read_write_availability.png' | relative_url }}" alt="Read and write availability levels of the 12 evaluated edge blockchain network designs">
        <figcaption>
          Read and write availability levels across the 12 designs under the five failure scenarios.
        </figcaption>
      </figure>
    </div>

    <div class="finding">
      <h3>Update availability: local versus global</h3>
      <figure class="figure figure--small">
        <img src="{{ '/assets/figures/update_availability.png' | relative_url }}" alt="Local and global update availability levels of the 12 evaluated edge blockchain network designs">
        <figcaption>
          Update availability is split into local propagation (within a cluster) and global propagation (across clusters). In-cluster designs propagate locally under most failures but not globally; cloud-only designs propagate in neither.
        </figcaption>
      </figure>
    </div>

    <p style="margin-top:1.5rem;">
      <strong>The trade-off:</strong> designs that maximise availability by placing full nodes on edge devices are
      also the most resource-intensive. They tend to restrict the consensus protocol to PoA. Designs that use
      cloud-only clients are resource-efficient but degrade badly under any connectivity failure. No single
      design dominates; the right choice depends on which failure modes the use case can absorb.
    </p>
  </div>
</section>

<section class="section">
  <div class="container">
    <h2>Abstract</h2>
    <p>
      Blockchains have been increasingly employed in use cases at the network's edge, such as autonomous vehicles
      and edge computing. These use cases usually establish new blockchain networks due to operation costs,
      performance constraints, and the lack of reliable connectivity to public blockchains. The design of these
      edge blockchain networks heavily influences the quality attributes of blockchain-oriented software deployed
      upon them. In this paper we present a taxonomy of edge blockchain network designs successfully used by the
      existing literature and analyse their availability when facing failures at nodes and networks. We believe
      this taxonomy benefits practitioners and researchers by offering a design guide for establishing
      blockchain networks for edge use cases.
    </p>
  </div>
</section>

<section class="section section--alt">
  <div class="container">
    <h2>BibTeX</h2>
    <pre class="bibtex"><code>@inproceedings{tran2021taxonomy,
  title     = {Taxonomy of edge blockchain network designs},
  author    = {Tran, Nguyen Khoi and Babar, Muhammad Ali},
  booktitle = {European Conference on Software Architecture},
  pages     = {172--180},
  year      = {2021},
  doi       = {10.1007/978-3-030-86044-8_12}
}</code></pre>
    <p class="doi-line">
      DOI: <a href="https://doi.org/10.1007/978-3-030-86044-8_12" rel="noopener">10.1007/978-3-030-86044-8_12</a>
    </p>
  </div>
</section>