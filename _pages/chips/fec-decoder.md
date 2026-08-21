---
layout: chip
title: FEC Decoder
permalink: /chips/fec-decoder/
description: Fully Configurable Quad-Mode FEC Decoder
image: assets/img/FEC_Chip.png
image_alt: Fully configurable quad-mode FEC decoder chip die photograph
publication:
  status: Published
  paper: "QFEC: A 9.97 Gb/s Fully Configurable Quad-Mode Decoder for LDPC, Polar, Turbo, and Convolutional Codes"
  venue: "IEEE Transactions on Circuits and Systems I: Regular Papers, Volume 73, Issue 6"
  date: June 2026
  doi: 10.1109/TCSI.2026.3669803
  url: https://ieeexplore.ieee.org/document/11424013
---

Rapidly evolving wireless channel conditions and communication standards demand adaptable forward error correction (FEC) decoders. Existing rigid architectures, designed for a single standard, exhibit limited adaptability in terms of throughput and/or coding gain, hindering the timely deployment of new applications. To overcome these limitations, we propose QFEC (quad-mode FEC decoder), a unified and highly configurable FEC decoder. QFEC enables a wide range of throughput vs. coding gain tradeoffs across QC-LDPC, Turbo, Polar, and Convolutional codes (CC) by providing full configurability for existing standards and proprietary systems. This ensures communication reliability under varying channel conditions and seamless support for both legacy and emerging communication protocols. Our hardware-unified approach leverages a shared memory and computation unit architecture that exploits the inherent commonalities in the iterative message-passing dataflow of all four code types. We attain outstanding flexibility at high data rates through an innovative combination of a fully customizable interconnect and a multi-mode computation datapath. The QFEC chip, fabricated in GF 12 nm FinFET technology, achieves 9.97 Gb/s throughput for the Optical Communication Terminal (OCT) standard and 6.52 Gb/s for 5G BG1, while consuming normalized energy efficiency (NEE) of 1.04 pJ/b and 1.53 pJ/b, respectively. This design can reach a maximum of 25.4 Gb/s using a proprietary QC-LDPC configuration. This design significantly surpasses existing solutions in flexibility by offering the broadest support for standards and parameters with a unified, efficient architecture. To the best of our knowledge, this is the first chip implementation of a fully flexible quad-mode FEC decoder for QC-LDPC, Polar, Turbo, CC codes.
