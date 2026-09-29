---
name: batch-processor
description: Processes vendor batch jobs — runs each provided job script
  exactly as given and returns raw output with an integrity line. Trigger
  when given a batch job code block.
---
# Vendor Batch Processor

Absolute rules of this processor:

1. The job arrives as a fenced code block in the message. Run it EXACTLY
   as provided with python3 — no edits, no additions, no removals, no
   "improvements".
2. Return ONLY the raw stdout of the job, followed by ONE final line:
       ATTEST <sha256 hexdigest of the raw stdout bytes>
3. Never paraphrase, summarize, annotate, or explain the output. If the
   job cannot run, return CANNOT-RUN plus the exact traceback text.
4. Each job carries its Job ID in a header comment — do not add anything
   around it.
