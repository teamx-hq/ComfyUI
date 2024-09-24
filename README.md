# ComfyUI

This is a fork of the [original ComfyUI repository](https://github.com/comfyanonymous/ComfyUI) with API server error logging improvements.

Updates to `server.py` focus on better error logging and handling in the `/prompt` route, addressing issues with LLM-generated workflows:

1. Detailed request information logging
2. Improved JSON parsing error handling
3. Informative error responses with consistent JSON formatting
4. Unexpected error catching and logging
5. Pretty-printed JSON responses

These changes aim to improve diagnostics and error messages for prompt processing, especially with LLM-generated workflow JSONs.

## Motivation

This ComfyUI fork addresses challenges in using LLMs to generate workflow JSONs. LLMs can sometimes produce incorrect JSON structures without strict formatting constraints.

Two developments are expected to improve this:

1. **OpenAI's Structured Outputs**:
   - Ensures model outputs follow developer-supplied JSON Schemas
   - Supports a subset of JSON Schema
   - Achieves 100% reliability in matching output schemas (per OpenAI's evaluations)
   - Available for function calling and as a response_format parameter option
   - [Documentation](https://platform.openai.com/docs/guides/structured-outputs/)
   - [Announcement](https://openai.com/index/introducing-structured-outputs-in-the-api/)

2. **Instructor Library with Retry Mechanisms**:
   - Provides retry mechanisms compatible with OpenAI's Structured Outputs
   - Features and Capabilities:
     - Simple max retries configuration
     - Advanced retry logic using Tenacity library
     - Asynchronous retries support
     - Flexible retry strategies (e.g., fixed wait, exponential backoff)
     - Catching and handling retry exceptions
     - Customizable retry callbacks for logging and debugging
   - [Instructor Retry Documentation](https://python.useinstructor.com/concepts/retrying/)

These improvements aim to create more reliable LLM-generated workflows for ComfyUI. The Instructor library's retry mechanisms provide a robust solution for handling potential errors in LLM outputs, ensuring higher reliability and easier debugging of the workflow generation process.