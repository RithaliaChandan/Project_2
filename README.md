Project — Rescale to Reference
Author: Chandan Rithalia
Date: 24/11/2025

1. Objective
   To rescale fragment lengths from the query BED file so that their normalized distribution matches the reference histogram. This is achieved using sampling probabilities and downsampling based on the ratio of reference 
   frequencies to query frequencies.

2. Steps

   2.1 Load reference histogram
       - Read reference.hist file.
       - Store length → frequency values.
       - Convert frequencies to a dense NumPy array.

   2.2 Count query fragment lengths
       - Read query.bed.gz.
       - Compute fragment length (end − start).
       - Keep lengths ≤ maximum reference length.
       - Build frequency counts and normalized length distribution.

   2.3 Compute sampling probabilities
       - For each length L:
           prob[L] = min(1, reference_freq[L] / query_freq[L])

   2.4 Perform sampling
       - Re-read query.bed.gz.
       - For each fragment:
           * Generate a random number.
           * Keep fragment if random < prob[L].
       - Store sampled fragment lengths.

   2.5 Build distributions
       - Normalize:
           * Query histogram
           * Sampled (rescaled) histogram
           * Reference histogram

   2.6 Plot distributions
       - Plot all three curves:
           * Query
           * Reference
           * Rescaled
       - X-axis = fragment length
       - Y-axis = normalized frequency

3. Script Used
   - Main Python script:
       * Loads reference
       * Calculates probabilities
       * Performs downsampling
       * Builds histograms
       * Plots final curves

4. Input
   - reference.hist
   - query.bed.gz

5. Output
   - Distribution plot comparing:
       * Query
       * Reference
       * Rescaled distributions

6. Conclusion
   The script provides a simple method to downsample query fragment lengths so their distribution matches the reference histogram, enabling standardized fragment length analysis.
