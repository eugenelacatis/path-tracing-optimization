# Learning Path

Read each item when its milestone is up next, not all at once. Every stage ends with something you can run.

Hardware targets: RTX 2070 Super (Turing, sm_75), RTX 5070 (Blackwell, sm_120).

---

## Stage 0: CUDA fundamentals (Week 1, overlaps Stage 1)

Skip what CMPE214 lectures already cover.

- **CUDA C++ Programming Guide**: Programming Model, Programming Interface, Hardware Implementation, Performance Guidelines.
  https://docs.nvidia.com/cuda/cuda-c-programming-guide/
- Concepts to be able to explain out loud: warps and SIMT, warp divergence, occupancy, coalesced memory access, shared memory, registers per thread and spilling.
- **Nsight Compute quickstart**: profile any small kernel and read the "Speed of Light" and "Warp State Statistics" sections.
  https://docs.nvidia.com/nsight-compute/

**Done when:** you can profile a kernel and explain why it is memory-bound or compute-bound.

---

## Stage 1: Ray tracing basics on CPU (Week 1, ~2 days)

- **Ray Tracing in One Weekend** (Peter Shirley), book 1.
  https://raytracing.github.io/
- Then skim book 2, **The Next Week**, for its BVH chapter only.

**Done when:** you render the final spheres scene to a PPM image on the CPU.

---

## Stage 2: Port to CUDA, the baseline megakernel (Week 2)

- **Accelerated Ray Tracing in One Weekend in CUDA** (Roger Allen, NVIDIA Developer Blog).
  https://developer.nvidia.com/blog/accelerated-ray-tracing-cuda/
- Build the benchmark harness now:
  - CUDA events for timing, warmup runs excluded
  - fixed scenes, camera, resolution, and samples per pixel
  - a high-spp reference image for each scene
- **FLIP** image-error metric (NVIDIA Research):
  https://github.com/NVlabs/flip

**Done when:** the CUDA version matches the CPU image, and the harness prints samples/sec and a FLIP score.

---

## Stage 3: GPU BVH (Weeks 3-4)

- **PBRT 4th ed.**, Chapter 7 "Primitives and Intersection Acceleration" (BVH, SAH).
  https://pbr-book.org/4ed/contents
- **Thinking Parallel, Parts I-III** (Tero Karras, NVIDIA Developer Blog): GPU BVH traversal and Morton-code construction.
- Paper: Karras, *Maximizing Parallelism in the Construction of BVHs, Octrees, and k-d Trees* (HPG 2012). This is the LBVH method.
- Mesh loading: tinyobjloader to start; move to glTF (tinygltf) when you need Sponza or Bistro.

**Done when:** Sponza renders, and you have a chart of traversal speed with and without the BVH.

---

## Stage 4: Monte Carlo path tracing theory (Weeks 3-5, read alongside Stage 3)

- **PBRT 4th ed.**, Chapters 2 (Monte Carlo integration), 4 (radiometry, skim), 13 (light transport / path tracing).
- **Ray Tracing: The Rest of Your Life** (book 3 at raytracing.github.io): importance sampling, explained in a more approachable way.

**Done when:** your tracer supports diffuse and specular materials with next-event estimation (direct light sampling).

---

## Stage 5: Wavefront path tracing (Weeks 5-6)

- Paper: Laine, Karras, Aila, *Megakernels Considered Harmful: Wavefront Path Tracing on GPUs* (HPG 2013).
- **Ray Tracing Gems II**, the chapters on GPU path tracer architecture. Free PDF:
  https://www.realtimerendering.com/raytracinggems/
- Concepts: ray queues, stream compaction, atomics for queue counters, sorting rays by material.

**Done when:** you have Nsight Compute screenshots of megakernel vs. wavefront (branch efficiency, occupancy, warp stall reasons) plus a throughput chart.

---

## Stage 6: OptiX and RT cores (Weeks 7-8)

- **OptiX SDK**: install it and build the `optixPathTracer` sample first.
  https://developer.nvidia.com/rtx/ray-tracing/optix
- **Ingo Wald's OptiX 7 course**: a step-by-step tutorial that still applies to current OptiX versions.
  https://github.com/ingowald/optix7course
- Concepts: acceleration structures (GAS/IAS), the shader binding table, raygen / closest-hit / miss programs.

**Done when:** the same scenes render through OptiX, with a chart comparing your BVH and OptiX on the 2070 Super and the 5070.

---

## Stage 7: Fewer samples, same quality (Week 9, pick one)

**Option A, ReSTIR DI (stretch goal):**
- Paper: Bitterli et al., *Spatiotemporal Reservoir Resampling for Real-Time Ray Tracing with Dynamic Direct Lighting* (SIGGRAPH 2020).
- **A Gentle Introduction to ReSTIR** (SIGGRAPH 2023 course notes). Read these before the paper.

**Option B, denoiser (fallback):**
- The OptiX built-in AI denoiser (`optixDenoiser` sample in the SDK).

**Done when:** a chart shows FLIP error vs. render time, with and without the technique.

---

## Reference shelf (not sequential)

- **Ray Tracing Gems I & II**, free PDFs: https://www.realtimerendering.com/raytracinggems/
- **PBRT 4th ed.**: https://pbr-book.org/
- **CUDA Best Practices Guide**: https://docs.nvidia.com/cuda/cuda-c-best-practices-guide/
- Test scenes: McGuire Computer Graphics Archive (Sponza, Cornell box), https://casual-effects.com/data/ ; Amazon Lumberyard Bistro (from NVIDIA ORCA).
