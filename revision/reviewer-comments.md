# Reviewer comments — JAWRA MS 8299185

_Manuscript_: "A real time reservoir inflow forecast evaluation framework"
_Journal_: Journal of the American Water Resources Association
_Decision_: Major revision requested
_Date sent_: 12 May 2026
_Handling editor_: Dr. William H. Farmer
_Revision due_: August 10, 2026 (extension available on request)
_Authors_: Cameron Bracken, Youngjun Son, Vince Tidwell, Nathalie Voisin

Any revisions will be re-reviewed before a final decision.

Reviewer 2's report was submitted as an attached file rather than inline text and is not part
of the decision letter. It is now in this directory as `2025-bracken-review-RL.pdf` and is
transcribed below.

---

## Handling editor comments

The manuscript titled "A real-time reservoir inflow forecast evaluation framework" is
well-prepared, and I see little barrier to imminent publication. Because of the
variability of initial responses, I've had four qualified reviewers consider this
manuscript, and their comments are included below. All provided useful comments (and
praise).

The greatest barrier, from my reading of the manuscript and review of the comments, is
the question of novelty and reproducibility. Reviewers 1, 3, and 4 note that there is no
distinct statement of novelty, with reviewer 3 particularly noting that the manuscript
seems to suggest that the framework is the novelty without fully describing the novelty.

To me, this suggests a critical point for decision-making is missing. The reviewers all
recognize some value here, but struggle to determine if it rises to the level of
publication. I see value and am thus deferring to the assumption that the authors will be
particularly attentive in their responses to the reviewers.

Any revisions will be re-reviewed before a final decision about publication is made.

---

## Reviewer 1

### General

This study presented a real time reservoir inflow forecast evaluation framework, which
included forecast verification and validation, as well as other qualitative or specialized
metrics of forecast quality. This evaluation framework was applied to three reservoirs in
the Great River Hydro system on the Connecticut River in the Northeast U.S. The goal of
this framework is to provide hydropower operators with information necessary for
evaluating how much a particular forecast product will improve their operations and
ultimately inform ongoing investment decisions.

The topic and the contents are relevant, and it is very interest for hydropower operators
and decision-makers. However, the novelty and main contributions of this study are
unclear. The commercial forecasts (A, B), the GRH in-house forecast, watershed information
etc. should be described in detail. The paper is poor organized and needs further
improvement by responding the following comments. Further work is deserved for more
analysis and discussion. Therefore, I recommend to reject in current version.

### Main comments

__R1.1__ The novelty and main contributions of this study are unclear. Please explain and
discuss in detail.

__R1.2__ Lines 70-72: "'persistence' forecasts which use the last observed value carried
out for all future timesteps to get a sense of the arguably worst possible forecast.
Persistence is a competitive benchmark for short term operations, from hours to 2-day
horizons". However, Fig. 3 and Fig. 4 show that 10-day and months "persistence forecasts"
as benchmark which is unrealistic in practice.

__R1.3__ What are the main operation problems of these hydropower stations? Which
forecasting scheme is used in practice?

__R1.4__ Two commercial forecasts (A, B) and the GRH in-house forecast (GRH) should be
described in detail, such as what type of hydrologic model used? How about the calibration
and validation results, what type input data requirement etc.

__R1.5__ Three main hydropower producing dams in the system, Wilder, Bellows Falls, and
Vernon (Figure 2) as well as three main tributaries, the Ottauquechee, Sugar and White
Rivers. The watershed information, such as area, river length etc. should be described in
detail.

__R1.6__ In Table 1, the NSE values of forecast scheme A at Wilder, Bellows and Vermon
watersheds are 0.72, 0.55, 0.81, respectively. Please check the evaluation results. The
forecasting accuracy at the Bellows might high than that at the Wilder.

__R1.7__ The format of Tables in the manuscript are poorly designed and needed be changed.

__R1.8__ The figures also need be redrawn.

---

## Reviewer 2

_Source_: `2025-bracken-review-RL.pdf` (submitted as an attachment).
_Recommendation: minor revision._

### Summary

Thank you for the opportunity to review this manuscript which presents a framework for
real-time evaluation of reservoir inflow forecasts, demonstrated on the Great River Hydro
system on the Connecticut River. The paper addresses a practical and important gap: how
hydropower operators can systematically assess whether new forecast products justify their
cost. The iterative approach with direct operator feedback is sensible and the tailored
exceedance metric is a good example of translating generic forecast quality into
operationally relevant information. I have two major comments regarding the need to engage
with the forecast value literature given the paper's stated goal of informing investment
decisions, and the positioning of the contribution. I also have some minor comments on
clarity, completeness, and technical accuracy. The core work is solid and the practical
contribution is genuine. Assuming the major comments are addressed I recommend this
manuscript is accepted with minor revision.

### Major comments

__R2.1__ The stated goal of the framework is to help operators evaluate whether a forecast
product will improve operations enough to justify investment. The paper does not include any
assessment of forecast value and the authors acknowledge this gap (L172–177), framing it as
"an important next step." I appreciate this is a difficult problem, but the paper needs to at
least engage with the existing forecast value literature and discuss how the presented
metrics relate to the investment question. There is an established body of work on forecast
value, from Thompson and Brier's (1955) first quantitative treatment through to more general
decision-theoretic approaches such as Laugesen's (2023, 2026) Relative Utility Value method.
The authors do not need to perform a full value assessment, but they should reference this
literature, discuss how it connects to their framework, and provide operators with at least a
conceptual pathway from the metrics presented to the investment decision the paper is
motivated by.

__R2.2__ The paper would benefit from clearly articulating what is new relative to existing
frameworks. The five-step iterative process (collect data, compute metrics, visualise, solicit
feedback, iterate) reads more as standard good operational practice than a novel framework
contribution. I feel that the tailored metrics and operator feedback loop are where the
genuine contribution lies, especially in the real-time context, and these deserve more
prominence and deeper treatment.

### Minor comments

__R2.3__ (L2, Title) "real time" should (perhaps) be hyphenated as "real-time" when used as
an adjective (also applies throughout the manuscript, e.g. L44, L48, L50, L110, L116).

__R2.4__ (L12–13) The sentences seem to imply that we should expect verification methods to
improve alongside improvements in forecasts, but this isn't the case. Also, the first sentence
is about forecast and scheduling methods but the second sentence links it to operational
paradigms somewhat abruptly. Suggest restructuring so the research gap is clearer.

__R2.5__ (L42–44) The distinction between deterministic and probabilistic is important and
well noted. However, the dismissal of ensemble evaluation metrics seems premature given that
the authors later suggest probabilistic forecasts may help (L170). Consider briefly noting
what ensemble metrics could be added if ensemble forecasts were available.

__R2.6__ (L45–47) The argument against hindcast evaluation is reasonable but somewhat
overstated. Hindcast evaluations do not necessarily require operators to re-operate the
system, especially if verifying forecasts of environmental variables such as inflows, which
you are. Suggest softening this claim or explaining how operators are in the loop for the
inflow forecasts. The first major comment above may be relevant here.

__R2.7__ (L71) Describing persistence as "arguably worst possible forecast" is incorrect.
Persistence is a competitive benchmark for short lead times as the authors themselves note in
the next sentence. Climatology is typically considered the lower bound for longer horizons.
Suggest rephrasing to "a simple but competitive benchmark."

__R2.8__ (L80–81) A triangular smoother is reasonable but the choice of window width is not
discussed. The smoothing window will affect the comparison with forecasts and should be
selected with care. Please note the window used and perhaps the sensitivity to this choice on
your findings.

__R2.9__ (L92) "King-Gupta Efficiency" should be "Kling-Gupta Efficiency." Also, "(refs)" is
a placeholder that needs to be replaced with actual references (Gupta et al. 2009 presumably).

__R2.10__ (L92–93) The claim that KGE is not skewed by large values while NSE and RMSE are
requires clarification. KGE and NSE both use correlation as a component. The relevant
difference is that KGE decomposes performance into correlation, variability ratio, and bias
ratio rather than using squared error. The statement as written is misleading.

__R2.11__ (L95–96) The KGE threshold of -0.41 is attributed to comparing against the mean of
observations but the Knoben et al. (2019) citation is on L97, not adjacent to the claim.
Consider restructuring so the citation directly supports the threshold statement.

__R2.12__ (L98–99) "The bias of a single forecast point is the difference between observed and
forecasted values" defines error (sometimes called residual), not bias. Bias is a systematic
tendency. Suggest correcting the definition.

__R2.13__ (Eq. 3) The Pearson correlation coefficient formula is missing a summation over the
second term of denominator.

__R2.14__ (L107) 589 megawatts of "nominal" hydropower capacity. Is this installed capacity or
average generation? Please clarify.

__R2.15__ (L109) Add a sentence describing how these 3 sites are related, given they are
downstream from one another one could assume they are operated jointly. Also good to note why
you chose these sites over all the other sites (green dots in the figure).

__R2.16__ (L117) Anonymising the commercial forecast products is understandable but limits
reproducibility. Consider at minimum describing the general class of model used by each (e.g.,
physics-based, statistical, machine learning) so readers can contextualise the results.

__R2.17__ (Figure 1) Y-axis units are "cfs" (cubic feet per second). Consider also providing
SI units for international readers.

__R2.18__ (L134) "Forecasts tend to perform worse in the winter which is the wet season and
worse in the summer which is the dry season." This says forecasts perform worse in both wet
and dry seasons. Please clarify when forecasts actually perform well and why. The following
sentence about snow melt season partially addresses this but the logic is unclear.

__R2.19__ (L146) The 0.5 foot (≈15 cm) operating range is an important constraint that
motivates a strong tailored metric. However, the forebay exceedance analysis assumes an
inflow=outflow condition which is operationally unrealistic as the authors note. It would
strengthen the analysis to discuss how operators actually deviate from this assumption and
what the real-world exceedance rates might be.

__R2.20__ (L178–182) The discussion on limitations of real-time vs hindcast evaluation is
good. Consider also noting the limitation that almost two years of data may not capture the
full range of extreme events which are often the conditions where forecast quality matters
most for operational decisions.

### Recommendation

Minor revision. The practical application and operator engagement aspects are valuable, and
the tailored metrics are a genuine contribution. The paper needs to be better positioning,
particularly against the forecast value literature to connect the presented metrics to the
investment decisions the paper is motivated by. These are framing and positioning issues
rather than fundamental methodological concerns.

---

## Reviewer 3

### General

Overall, this manuscript proposes a framework for realtime reservoir inflow forecast
evaluation. The proposed framework was applied to three reservoirs on the Connecticut
River, then several usefull suggestions are found. However, proposed framework itself is
not well described, such as what is new, different from existing ones, and comparison of
past studies are insufficient.

### Specific comments

__R3.1__ (l47) "market prices" — Could you please clarify what it means?

__R3.2__ (l50, §2.1 real time inflow forecast evaluation) Step 1 through 3 are so general.
I assume that steps 4 and 5 are unique points in this manuscript. Please provide a more
detailed explanation of how feedback is reflected in step 4.

__R3.3__ (l62, "5. Iterate") This implies that at least one year learning period is
required. Is this understanding correct?

__R3.4__ (l105, result of case study) Were all the results derived through the proposed
framework? If so, please compare those result with those obtained via "traditional"
methods. This conmparison may enable to enhance the effectiveness of the proposed
framework.

__R3.5__ (l139, §3.1 Tailored metrics) Please explain the advantage of introducing
tailored metrics. For example, it would be helpful to show a case where using tailored
metrics led to a different forecast onclusion compared to general metrics.

---

## Reviewer 4

_Recommendation: minor revision._

### General

The manuscript titled "A real time reservoir inflow forecast evaluation framework"
presents a general framework for evaluating reservoir inflow forecasts in real time, with
application to three hydropower dams in the Great River Hydro system. The overall idea is
relevant and practically useful for hydropower operators seeking to assess competing
forecast products. The paper is generally well-written, and the iterative,
operator-inclusive evaluation approach adds value. However, several methodological details
require clarification. I recommend a minor revision.

### Major comments

__R4.1__ Lines 80-81 recommend a triangular smoother for calculated inflows but do not
specify the smoothing window size (number of days or timesteps). This is a critical
parameter because the choice of window directly affects computed evaluation metrics. The
window size must be stated explicitly, and a sensitivity analysis or justification for the
chosen value would strengthen the paper.

__R4.2__ Line 116 states the evaluation ran from July 2023 to May 2025. The authors should
discuss whether this period captured any notable extreme hydrologic events (major floods,
drought conditions) and how climatologically representative it is relative to the
long-term record for the Connecticut River basin. This context is important for
understanding the generalizability of the approach.

__R4.3__ Line 117 The authors anonymize the two commercial forecasts as A and B. While
commercial confidentiality is understandable, the paper should provide at least a general
characterization of each forecast's methodology (e.g., physics-based,
machine-learning-based, hybrid, statistical). Without this, readers cannot interpret the
results in a broader methodological context or assess the generalizability of the
findings.

__R4.4__ The paper focuses only on deterministic forecast evaluation (lines 42-49). While
this is acknowledged, the framework could be briefly extended to probabilistic or ensemble
forecasts using metrics such as CRPS, reliability diagrams, or rank histograms. This would
make the description more complete and forward-looking, especially given the authors' own
statement that probabilistic forecasts are gaining in popularity.

### Minor comments

__R4.5__ (Introduction) Throughout the manuscript: "real time" should be hyphenated when
used as a compound adjective (e.g., "real-time evaluation"). Usage is inconsistent.

__R4.6__ (Methods, line 92) Remove the placeholder "(refs)" and insert the actual KGE
citation (Gupta et al. 2009).

__R4.7__ (Results and Case Study, Table 1) Consider adding RMSE or MAE values alongside
the existing metrics to provide a sense of forecast error magnitude in physical units.

__R4.8__ (Figure 5 caption) The caption does not specify that the error bars represent the
2.5th and 97.5th percentiles (as stated in the main text at lines 148-149). Figure caption
needs to be self-contained.

__R4.9__ (Discussion, lines 173-174) The authors note that coupling this evaluation with
hydropower scheduling models is an important next step. This point could be strengthened
by briefly discussing what such a coupling would entail and what data would be needed.

---

## Comment inventory

| Source | Comments | Recommendation | Theme |
|---|---|---|---|
| Editor | 1 | Major revision | Novelty and reproducibility |
| Reviewer 1 | 8 | Reject in current version | Novelty, provider/basin description, table and figure quality |
| Reviewer 2 | 20 | Minor revision | Forecast value literature, positioning, technical errors in methods |
| Reviewer 3 | 5 | Not stated | Novelty, framework description, tailored vs generic metrics |
| Reviewer 4 | 9 | Minor revision | Smoothing window, record representativeness, provider methods, probabilistic extension, minor edits |

Cross-cutting themes and where they appear:

| Theme | Comments |
|---|---|
| Novelty / positioning of the contribution | editor, R1.1, R2.2, R3 general, R3.4 |
| Forecast provider characterization | R1.4, R2.16, R4.3 |
| Smoothing window and sensitivity | R2.8, R4.1 |
| Persistence misdescribed / misapplied | R1.2, R2.7 |
| KGE citation and "King-Gupta" typo | R2.9, R4.6 |
| Tailored vs generic metrics | R2.2, R3.5 |
| Probabilistic / ensemble extension | R2.5, R4.4 |
| Record length and extreme events | R2.20, R4.2 |
| "real time" hyphenation | R2.3, R4.5 |
| Basin / site description | R1.5, R2.15 |

Reviewer 2 is the only reviewer to raise the __forecast value literature__ (R2.1), which is
the single largest addition to the manuscript, and the only one to check the equations
(R2.13, a real error in the Pearson formula). Reviewers 1 and 3 both call the framework's
novelty unclear; Reviewer 2 goes further and says where the contribution actually lies,
which is the framing adopted in the response.

Recommendations diverge sharply, from reject (R1) to minor revision (R2, R4). The editor's
letter treats novelty as the deciding issue, so that is where the response leads.
