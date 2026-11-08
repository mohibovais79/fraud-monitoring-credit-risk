## Shell command rules
- Never use python heredocs (python - <<EOF) or python -c with inline code.
- Write scripts to a file with the Write tool, then run the file.
- Never use shell brace expansion like {a,b}; write each path out explicitly.