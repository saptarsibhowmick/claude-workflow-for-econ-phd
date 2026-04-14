# Journal Profiles

> Agents read this file when calibrating peer review to a specific journal.
> Add or modify profiles for your target journals.

## How Profiles Work

When you run `/referee2` or simulated peer review targeting a journal, the Editor and referees adapt their priorities, bar, and checklists to that journal's review culture.

---

## Top 5

### AER (American Economic Review)
- **Bar:** Highest. Must advance understanding of an important question.
- **Referees prioritize:** Clean identification, robustness, external validity, policy relevance
- **Typical concerns:** Is the question first-order important? Is identification bulletproof? Are results driven by outliers?
- **Word limit:** ~12,000 words
- **Replication:** AEA Data Editor review mandatory. Replication package must pass audit.

### QJE (Quarterly Journal of Economics)
- **Bar:** Highest. Strong preference for surprising or counterintuitive findings.
- **Referees prioritize:** Novelty, clean research design, clear writing
- **Typical concerns:** Is this surprising? Could this be explained by selection?

### JPE (Journal of Political Economy)
- **Bar:** Highest. Values theoretical grounding alongside empirics.
- **Referees prioritize:** Connection to economic theory, magnitude interpretation
- **Typical concerns:** What model rationalizes these findings? Are magnitudes plausible?

### Econometrica
- **Bar:** Highest. Technical rigor is paramount.
- **Referees prioritize:** Methodological contribution, formal identification argument
- **Typical concerns:** Is the econometric approach novel? Are assumptions formally stated?

### REStud (Review of Economic Studies)
- **Bar:** Highest. High technical bar with broad appeal.
- **Referees prioritize:** Technical sophistication, broad interest
- **Typical concerns:** Is this of interest beyond the subfield?

---

## Top Field Journals

### JDE (Journal of Development Economics)
- **Bar:** High. Reduced-form empirical work is the core.
- **Referees prioritize:** Identification, mechanisms, policy relevance, context
- **Typical concerns:** Is the institutional setting well-described? Are mechanisms explored? External validity?
- **Word limit:** ~10,000–12,000 words
- **Notes:** Expects detailed institutional background. Heterogeneity analysis valued.

### AEJ:Applied (American Economic Journal: Applied Economics)
- **Bar:** High. Policy-relevant empirical work.
- **Referees prioritize:** Clean identification, magnitudes, policy implications
- **Typical concerns:** Magnitudes in economic terms, not just statistical significance

### AEJ:Policy (American Economic Journal: Economic Policy)
- **Bar:** High. Policy evaluation focus.
- **Referees prioritize:** Policy relevance, causal identification, welfare implications
- **Typical concerns:** What is the policy counterfactual?

### JEEA (Journal of the European Economic Association)
- **Bar:** High. Accepts both structural and reduced-form.
- **Referees prioritize:** European or broadly relevant settings, technical quality

### RESTAT (Review of Economics and Statistics)
- **Bar:** High. Empirical methods and applications.
- **Referees prioritize:** Methodological rigor, careful measurement

---

## Strong Field Journals

### JHR (Journal of Human Resources)
- **Bar:** Strong. Labor and education focus.
- **Referees prioritize:** Human capital, labor market outcomes, careful identification
- **Typical concerns:** Is the labor market mechanism clear?

### WBER (World Bank Economic Review)
- **Bar:** Strong. Development policy focus.
- **Referees prioritize:** Policy relevance, developing country context, data quality
- **Typical concerns:** Generalizability beyond the specific setting

### JPubE (Journal of Public Economics)
- **Bar:** Strong. Public finance and public policy.
- **Referees prioritize:** Fiscal implications, welfare analysis, public goods

---

## Adding Custom Profiles

Copy this template and fill in for any target journal:

```markdown
### [JOURNAL NAME]
- **Bar:** [Highest / High / Strong]
- **Referees prioritize:** [What matters most]
- **Typical concerns:** [Common objections]
- **Word limit:** [If applicable]
- **Notes:** [Any special conventions]
```
