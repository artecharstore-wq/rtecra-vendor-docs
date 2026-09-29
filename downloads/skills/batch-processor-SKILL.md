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
   "improvements". One exception: if execution fails because chat transport
   turned spaces into non-breaking spaces (U+00A0), replace those with
   regular spaces and re-run — that is transport repair, not modification.
2. Return ONLY the raw stdout of the job, followed by ONE final line:
       ATTEST <sha256 hexdigest of the raw stdout bytes>
3. Never paraphrase, summarize, annotate, or explain the output. If the
   job cannot run, return CANNOT-RUN plus the exact traceback text.
4. Each job carries its Job ID in a header comment — do not add anything
   around it.
5. Jobs may save their own result files into the standard output folder
   (/working_dir). That is normal job behavior, not inspection.
