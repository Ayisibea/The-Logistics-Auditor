# Veridi Logistics — Delivery Performance Audit

## A. Executive Summary

An audit of 96,478 delivered orders reveals that Veridi Logistics has a systemic
delivery accuracy problem driven by inaccurate estimates, not just late shipments.
Super Late orders (>5 days late) score 1.79 out of 5 versus 4.29 for On Time orders —
a 2.50-point drop proving that broken delivery promises, not just delays, are driving
negative reviews. Geographic analysis shows northeastern states, particularly Alagoas (AL)
and Maranhão (MA), are disproportionately affected with the worst on-time rates and lowest
satisfaction scores. The root cause is systemic over-promising — the estimation algorithm
tells customers packages will arrive 11.28 days earlier than they actually do.

---

## B. Project Links

- **Notebook:** [Google Colab Notebook](https://colab.research.google.com/drive/14pk3x6geLSnUVJBJU4rYK4imggcsFb8G?usp=sharing)
- **Dashboard:** [Power BI Dashboard](https://app.powerbi.com/view?r=eyJrIjoiOWE1OTMzOTYtZjU2NS00MTAzLWFhYWItMjJmMzc0OGU3MjhjIiwidCI6Ijk0MWJiZjVmLWYyYzAtNDg3NS1hMjRjLTY5MDc4NjVkMjUxYSIsImMiOjh9)
- **Presentation:** [Google Slides Deck](https://docs.google.com/presentation/d/e/2PACX-1vRfR263H-t4gDkV67bKlGK9tPbihNZ6j1w_Jr2iT5p-okdzD6IMvYefwNbL0jV-wg/pub?start=false&loop=false&delayms=3000)

---

## C. Technical Explanation

### Data Cleaning

- **Duplicate reviews:** Some orders had multiple reviews — deduplicated by keeping
  the most recent review per `order_id` before joining, preventing row inflation.
- **Undelivered orders:** Orders with status `canceled` or `unavailable` were excluded
  from the delay analysis to ensure only completed deliveries were measured.
- **Date conversion:** All timestamp columns were converted to `datetime` format before
  calculating `days_difference` and `promise_gap` metrics.
- **Missing translations:** Portuguese product category names were translated to English
  using the included `product_category_name_translation.csv`. Any untranslated categories
  retained their original Portuguese name as a fallback.
- **Relative paths:** This notebook is designed for Google Colab. Mount Google Drive
  and place the Olist dataset files in a folder called `archive` in My Drive before running.

### Candidate's Choice — The Promise Score

The Promise Score measures how reliably the system sets delivery expectations per state,
on a scale of 0–100 (higher = more reliable). Rather than simply identifying which states
receive late deliveries, this metric quantifies how badly the estimation algorithm is
miscalibrated per region.

**Why it matters to the business:** Knowing that deliveries are late is useful. Knowing
by how much the system is systematically lying gives operations a concrete number to fix.
The analysis found that Alagoas (AL) scored the worst at 77.1, with 22.92% of orders
over-promised — nearly 3x the national rate of 7.6%. The national average promise gap
is −11.28 days, meaning customers are routinely told their package will arrive 11 days
earlier than it actually does.

**Business recommendation:** Simply adding a region-specific buffer to delivery date
estimates — without changing any logistics operations — would significantly reduce
negative reviews by aligning customer expectations with reality.

---

## Pre-Submission Checklist

- [x] My GitHub Repo is Public
- [x] I have uploaded the `.ipynb` notebook file
- [x] I have uploaded a PDF export of the notebook
- [x] I have NOT uploaded the raw dataset
- [x] My code uses relative paths (noted above)
- [x] My Dashboard link is publicly accessible
- [x] My Presentation link is publicly accessible
- [x] I have updated this README with my Executive Summary and technical notes
- [x] I have completed User Stories 1–4
- [x] I have completed the Candidate's Choice challenge and explained it above
