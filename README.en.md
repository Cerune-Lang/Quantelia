# Quantelia

[日本語](README.md) | English

Quantelia is an experimental general-purpose numerical computing library for [Cerune](https://github.com/Hokutaka/Cerune).

**Numerical computing you can observe.**

Quantelia aims to make numerical results, computational rules, numerical behavior, and execution paths understandable and verifiable.

## Principles

- **Independent:** Quantelia does not depend on [Nerune](https://github.com/Hokutaka/Nerune) or contain machine-learning-specific concepts.
- **Observable:** Document types, shapes, operation semantics, floating-point behavior, and errors. Provide small reproducible examples.
- **Measurement separated from computation:** Timing and backend benchmarking belong to the host tooling or [Whitebase](https://github.com/Hokutaka/Whitebase), not to Quantelia's core numerical APIs.
- **Incremental:** Clearly distinguish implemented features from plans and check numerical correctness across available Cerune execution paths.

## Current scope

Development starts with an experimental `f32` tensor backed by a flat array and a shape array. The API is provisional.

Planned steps include shape validation, elementwise operations, reductions, linear algebra, and basic statistics.

## Try it

Install Cerune, then from the Quantelia repository root:

```sh
cerune check examples/basic_tensor.ceru
cerune run examples/basic_tensor.ceru
```

## Related projects

- [Cerune](https://github.com/Hokutaka/Cerune): language, intermediate representations, execution and code generation
- [Nerune](https://github.com/Hokutaka/Nerune): machine learning library that may consume Quantelia
- [Whitebase](https://github.com/Hokutaka/Whitebase): backend comparison and benchmarking
- [Tint*](https://github.com/Hokutaka/Tint-St): compiler observability

## Name

Quantelia combines “Quant,” for quantitative computation, and “Camellia,” the flower.

## License

MIT License
