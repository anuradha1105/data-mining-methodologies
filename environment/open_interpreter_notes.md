We are using a local workflow inspired by `open-interpreter` to run AI-guided code generation and debugging in a controlled environment.

Why mention this:
- The assignment suggests using GPT-5 or Claude plus open-interpreter to iterate safely without API limits.
- The idea is: ask the model to propose code, then run/verify the code in a sandbox environment (like a Docker container) instead of trusting the model blindly.
- In this project, we still manually review and execute all code in Google Colab, and document fixes.
