# Identical Parallel-Machine Scheduling with Worker Assignment

**Advanced Algorithms Group Project**  
University of Sharjah · College of Computing and Informatics  
Dr. Mehdi Jemmali · April 2026

**Authors**
- Maitha Alawadhi (U25200153): H1, H2, Simulated Annealing, MILP
- Sana Aziz (U25105011): H3, H4, Genetic Algorithm

---

## Problem

Assign *n* jobs to *m* identical parallel machines and distribute *W* workers among machines to minimise the makespan. Processing time of job *i* on a machine with *u* workers:

```
p_i(u) = A_i + B_i / (E_i · u)
```

---

## Algorithms Implemented

| Algorithm | Type | Author |
|-----------|------|--------|
| H1 : LPT + RBR | Constructive heuristic | Maitha |
| H2 : SPT + RBR | Constructive heuristic | Maitha |
| H3 : LB-guided decreasing + MFR | Constructive heuristic | Sana |
| H4 : LB-guided increasing + MFR | Constructive heuristic | Sana |
| SA : Simulated Annealing | Metaheuristic | Maitha |
| GA : Genetic Algorithm | Metaheuristic | Sana |
| MILP : Linearised exact model | Exact method (HiGHS) | Maitha |

---

## How to Run

1. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

2. **Open the notebook**  
   Upload `Adv_Algo_Project.ipynb` to Google Colab or run locally with Jupyter.

3. **Run cells in order**:
   - Cells 1–18: shared infrastructure (Instance, Solution, evaluator, sanity checks)
   - Cells 20–36: H1, H2, RBR, MFR
   - Cells 38–48: H3, H4, GA
   - Cells 50–58: Simulated Annealing
   - Cells 60–63: MILP
   - Cell 77: run main benchmark (H1/H2/SA/MILP) -> saves `benchmark_checkpoint.json`
   - Cell 79: run Sana's benchmark (H3/H4/GA) -> saves `benchmark_checkpoint_h3h4ga.json`
   - Last cell: combine both results -> exports `combined_benchmark_gaps.xlsx`

4. **Outputs**
   - `benchmark_checkpoint.json` contains raw results for H1/H2/SA/MILP (1,000 rows)
   - `benchmark_checkpoint_h3h4ga.json` contains raw results for H3/H4/GA (1,000 rows)
   - `combined_benchmark_gaps.xlsx` contains combined results, all 7 algorithms, 3 gap metrics

---

## Benchmark

- **Configurations:** I/P/6/3/10 and I/P/12/3/10 (Family H benchmark, Hu 1961)
- **Seeds:** 500 per configuration (1,000 instances total)
- **Gap metrics:**
  - Gap 1: `(Cmax − LB) / LB`  vs theoretical lower bound
  - Gap 2: `(Cmax − MILP) / MILP` vs proven optimum
  - Gap 3: `(Cmax − Best) / Best` vs best solution across all 7 algorithms

---

## Reproducibility

All algorithms use `numpy.random.default_rng(seed)` seeded per instance. Running the notebook top to bottom produces identical results on any machine.

---

## References

1. Hu, T.C. (1961). Parallel sequencing and assembly line problems. *Operations Research*, 9(6):841–848.
2. Chaudhry & Drake (2008). Minimizing total tardiness... *Int. J. Advanced Manufacturing Technology*, 38:1065–1075.
3. Kirkpatrick et al. (1983). Optimization by simulated annealing. *Science*, 220(4598):671–680.
4. HiGHS solver: https://highs.dev
