---
name: describe-image
description: Uses a local model to describe something about an image
license: MIT
compatibility: opencode
metadata:
  audience: tools
---

There is a local CLI tool describe_image that uses a local AI to describe an image. Don't use this tool in parallel or we might overwhelm our GPU.

```
describe_image <disk path> "<prompt to ask about details in image>"
```