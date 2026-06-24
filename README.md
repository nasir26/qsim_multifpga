# QSim Multi-FPGA

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

Dual-engine FPGA quantum circuit simulator: distributed exact statevector (28 qubits,
complex128) + MPS engine (500+ qubits) on 4× Xilinx Alveo U55C at C-DAC Noida.

**Author**: Nasir Ali — Centre for Development of Advanced Computing (C-DAC), Noida

## Overview

QSim Multi-FPGA provides a unified interface to two simulation backends that
complement each other's strengths:

| Engine | Max Qubits | Memory | Accuracy |
|--------|-----------|--------|---------|
| Statevector | 28 | $2^{28} \times 16$ B = 4 GB | Exact |
| MPS | 500+ | $O(n \cdot \chi^2 \cdot d^2)$ | Approximate (bond-dim limited) |

## Key Features

- Auto-routing: circuit sent to best engine based on qubit count and entanglement
- complex128 precision (float64 pairs) for statevector engine
- Distributed statevector across 4 Alveo U55C cards (top-2 qubit partition)
- 3-barrier shared-memory exchange for non-local gates
- Diagonal-gate local path: zero cross-card data movement for CP/RZ/CZ gates

## Requirements

- 4× Xilinx Alveo U55C, XRT 2.16.204
- Python 3.8+, NumPy, Qiskit

## Quick Start

```python
from qsim_multifpga import QSimMultiFPGA

sim = QSimMultiFPGA(num_cards=4)
result = sim.run(build_qft(n=20))
print(f"Fidelity: {result.fidelity:.12f}")  # 1.000000000000
sim.shutdown()
```

## Related Repositories

- [Multi-FPGA-QFT-Simulation](https://github.com/nasir26/Multi-FPGA-QFT-Simulation) — primary simulation codebase
- [FPGA_Based_30_Qubits_Statevector_Simulator](https://github.com/nasir26/FPGA_Based_30_Qubits_Statevector_Simulator) — single-card 30-qubit version

---

## Citation

If you use this work in your research, please cite:

```bibtex
@misc{nasirali_qsim_multifpga,
  author    = {Nasir Ali},
  title     = {qsim multifpga},
  year      = {2026},
  publisher = {GitHub},
  url       = {https://github.com/nasir26/qsim_multifpga},
  note      = {Centre for Development of Advanced Computing (C-DAC), Noida, India}
}
```

## License

This project is licensed under the MIT License — see [LICENSE](LICENSE) for details.\
© 2026 Nasir Ali, C-DAC Noida. All rights reserved.
