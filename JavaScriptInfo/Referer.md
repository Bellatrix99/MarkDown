## Referer

| 值                                             | 同源       | 跨源       | HTTPS→HTTP |
| :--------------------------------------------- | :--------- | :--------- | :--------- |
| `"no-referrer"`                                | -          | -          | -          |
| `"no-referrer-when-downgrade"` 或 `""`（默认） | 完整的 url | 完整的 url | -          |
| `"origin"`                                     | 仅域       | 仅域       | 仅域       |
| `"origin-when-cross-origin"`                   | 完整的 url | 仅域       | 仅域       |
| `"same-origin"`                                | 完整的 url | -          | -          |
| `"strict-origin"`                              | 仅域       | 仅域       | -          |
| `"strict-origin-when-cross-origin"`            | 完整的 url | 仅域       | -          |
| `"unsafe-url"`                                 | 完整的 url | 完整的 url | 完整的 url |

