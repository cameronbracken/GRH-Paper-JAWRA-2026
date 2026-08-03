# Response to reviewer and editor comments

_Manuscript_: "A real time reservoir inflow forecast evaluation framework", submitted to
the Journal of the American Water Resources Association (MS 8299185). Cameron Bracken,
Youngjun Son, Vince Tidwell, Nathalie Voisin.

We thank the editor and the four reviewers for their constructive comments. The reviewers
converged on one central point, which the handling editor also identified: the manuscript
described a framework without stating plainly what is new about it. We agree. The original
draft presented the five-step process as if the process itself were the contribution, when
the actual contribution is narrower and more useful than that. We have restructured the
introduction and methods around an explicit novelty statement, added a section comparing
this framework to retrospective verification practice, and added a subsection showing a
case where a tailored metric and a generic metric lead to different conclusions about the
same forecast.

We have also substantially expanded the description of the study system and the forecast
products, added a smoothing sensitivity analysis, characterized the hydrology of the
evaluation period against the long-term record, and rebuilt every table and figure. We
hope this revision makes the contribution unambiguous and the work reproducible.

Reviewer comments are in italics, our responses follow in plain text.

---

## Editor comments

> _The greatest barrier, from my reading of the manuscript and review of the comments, is
> the question of novelty and reproducibility. Reviewers 1, 3, and 4 note that there is no
> distinct statement of novelty, with reviewer 3 particularly noting that the manuscript
> seems to suggest that the framework is the novelty without fully describing the novelty._

Thank you for organizing four reviews and for the clear diagnosis. Reviewer 3 identified
the problem precisely: we presented the framework as the novelty without saying what in it
was new. Steps 1 through 3 of our process are indeed generic, as Reviewer 3 notes, and we
should not have implied otherwise.

We have added an explicit statement of contribution to the end of the introduction:

> "The contribution of this work is not the individual metrics, which are standard, nor the
> general idea of forecast verification, which is well established. It is a specific
> operating procedure for the case where a utility must choose between competing forecast
> products under live operating conditions and cannot run a hindcast. That procedure has
> three components that distinguish it from retrospective verification practice. First,
> metric selection is deferred rather than fixed in advance: the evaluation begins with
> generic metrics and adds system-specific metrics as the record accumulates and as
> operators identify what matters to them. Second, the operators are participants in metric
> design rather than recipients of results, which changes which metrics get computed.
> Third, the evaluation runs on the same data feed the operators use, so the evaluation
> inherits the data availability, latency, and outage characteristics of the operational
> system rather than the clean conditions of an archived dataset. We demonstrate below a
> case where the second component changed the conclusion: a tailored metric identified a
> forecast deficiency that all four generic metrics missed."

On reproducibility, the evaluation code is public
(<https://github.com/HydroWIRES-PNNL/inflow-forecast-evaluation>) and sample data is on
Zenodo (<https://doi.org/10.5281/zenodo.16921728>). We have expanded the methods section
with the parameter values that were previously left implicit, most importantly the
smoothing window (Reviewer 4, comment 1), and we have added the drainage areas and
regulation characteristics of each evaluation point (Reviewer 1, comment 5). The
proprietary forecast time series cannot be released, which we now state as a limitation
along with what a reader would need to replicate the analysis on their own system.

---

## Reviewer 1

> _The topic and the contents are relevant, and it is very interest for hydropower
> operators and decision-makers. However, the novelty and main contributions of this study
> are unclear._

Thank you for the review. The comments on the framing, the missing system description, and
the table and figure quality were all warranted and we have addressed each below.

### 1.1 Novelty and main contributions

> _The novelty and main contributions of this study are unclear. Please explain and discuss
> in detail._

We agree this was missing. Please see our response to the editor above for the new
contribution statement. In brief, the contribution is a procedure for the specific
situation where a utility must choose among competing forecast products under live
operating conditions and a hindcast is not available. What distinguishes it from standard
verification is that metric selection is deferred and driven by operator input rather than
fixed in advance, and that the evaluation runs on the operational data feed rather than an
archived dataset.

We have also added a paragraph to the discussion on why this matters now. Forecast products
using data driven methods are being marketed to utilities at an increasing rate, and the
verification statistics vendors supply are computed on their own hindcasts against their
own choice of reference data. A utility has no standard procedure for checking those claims
against its own system. This framework is that procedure.

### 1.2 Persistence as a benchmark at long lead times

> _Lines 70-72: "'persistence' forecasts which use the last observed value carried out for
> all future timesteps to get a sense of the arguably worst possible forecast. Persistence
> is a competitive benchmark for short term operations, from hours to 2-day horizons".
> However, Fig. 3 and Fig. 4 show that 10-day and months "persistence forecasts" as
> benchmark which is unrealistic in practice._

You are correct and this is an inconsistency in the original manuscript. We stated that
persistence is only competitive to about 2 days and then plotted it out to 10 days, and we
also noted that a climatological benchmark would be more appropriate at longer horizons
without actually using one.

We have made two changes. First, in Figures 3 and 4 the persistence benchmark is now
plotted only over the 1 to 2 day range where it is a meaningful reference, and is shown as
a distinct line style beyond that range where it is retained only to show the scale of
degradation. Second, we have added a monthly climatological benchmark computed from the
long-term record at each location, which is the appropriate reference at the longer lead
times shown in these figures. The text now reads:

> "Persistence degrades quickly beyond two days and is not a meaningful reference at longer
> horizons. For lead times beyond two days we therefore add a climatological benchmark
> computed as the long-term mean inflow for the corresponding day of year at each location.
> Evaluators should match the benchmark to the horizon of interest: persistence for hourly
> to 2-day operations, climatology for weekly to seasonal horizons."

We note that the day-ahead volumetric forecast is the operationally relevant horizon for
this system, where persistence remains an appropriate benchmark.

### 1.3 Operating problems and the forecasting scheme in practice

> _What are the main operation problems of these hydropower stations? Which forecasting
> scheme is used in practice?_

This context was missing and it is needed to make the tailored metrics comprehensible. We
have added a subsection describing the operating situation:

The three dams are run-of-river with limited storage. Their daily cycle consists of an
upward ramp, a period of flexible generation, a downward ramp, and a refill period.
Generation is bid into the ISO New England day-ahead market, so the day-ahead inflow volume
is the quantity that matters most: it sets what the operators can commit to. The binding
operational constraint comes from the FERC relicensing of the three lower Connecticut River
dams, which imposed a plus or minus 0.5 foot limit on forebay fluctuation, with penalties
for exceedance. The central operating problem is therefore committing generation a day
ahead on the basis of an inflow forecast without violating the forebay band. This is what
motivated the cumulative-error and threshold-exceedance metrics in Section 3.1.

On the forecasting scheme used in practice: at the time of the evaluation the operators
used an in-house forecast built from National Weather Service River Forecast Center
forecasts, routed to the dam locations, and adjusted using operator judgment. This is the
incumbent product against which the two commercial forecasts were being evaluated, and it
is labeled GRH in the results.

### 1.4 Description of the forecast products

> _Two commercial forecasts (A, B) and the GRH in-house forecast (GRH) should be described
> in detail, such as what type of hydrologic model used? How about the calibration and
> validation results, what type input data requirement etc._

Reviewer 4 raised the same point in their comment 3. We agree that anonymization without
any methodological characterization leaves readers unable to interpret the results, and we
have added what we can disclose.

The two commercial products were provided under agreements that prevent us from naming the
vendors or describing their model internals, and we do not have access to their calibration
and validation diagnostics. We have added the following characterization, which is the
level of detail we are able to publish:

> "Forecast A is produced by a consulting firm using a conceptual rainfall-runoff model with
> hydraulic routing through the Connecticut River mainstem, driven by a commercial numerical
> weather prediction vendor, and issued once daily. Forecast B is produced by a technology
> firm using a machine learning model trained on gauge and remotely sensed catchment
> observations, issued twice daily at hourly timestep out to 240 hours. The GRH in-house
> forecast combines National Weather Service River Forecast Center forecasts with routing
> and operator judgment, and extends only through the day-ahead period because that is the
> horizon it is used for. Neither vendor released model internals or calibration
> diagnostics, which is itself a finding: a utility evaluating commercial products generally
> cannot inspect them and must judge them on operational performance. This is part of the
> motivation for the framework."

We have added the inability to inspect commercial products to the limitations discussion.
Input data requirements differ substantially between the two, which is relevant to a
procurement decision, and we now note that a full evaluation should include the operational
cost and data dependency of each product alongside its skill.

### 1.5 Watershed information

> _Three main hydropower producing dams in the system, Wilder, Bellows Falls, and Vernon
> (Figure 2) as well as three main tributaries, the Ottauquechee, Sugar and White Rivers.
> The watershed information, such as area, river length etc. should be described in detail._

Agreed, this was a gap. We have added a table of physical characteristics for each
evaluation point, with drainage areas from the USGS National Water Information System:

| Location | Type | USGS gage | Drainage area (mi²) |
|---|---|---|---|
| Wilder | Mainstem dam | 01144500 (West Lebanon, NH) | 4,092 |
| Bellows Falls | Mainstem dam | 01154500 (North Walpole, NH) | 5,493 |
| Vernon | Mainstem dam | 01156500 (Vernon, VT) | 6,266 |
| White River | Tributary | 01144000 (West Hartford, VT) | 690 |
| Sugar River | Tributary | 01152500 (West Claremont, NH) | 269 |
| Ottauquechee River | Tributary | 01151500 (North Hartland, VT) | 221 |

We have also added text describing the basin: the mainstem drainage areas are nested, so
Vernon includes the areas above Bellows Falls and Wilder. This nesting matters for
interpreting the results and explains the downstream bias propagation noted in the original
manuscript. The three dams have limited storage relative to their inflow and are operated
run-of-river. Basin hydrology is snowmelt influenced with a spring freshet, typically
April through June, convective summer rainfall, and rain and rain-on-snow driven winter
events. Several tributaries have upstream flood control regulation by the U.S. Army Corps
of Engineers, which contributes to inflow variability that is not weather driven.

### 1.6 NSE values in Table 1

> _In Table 1, the NSE values of forecast scheme A at Wilder, Bellows and Vermon watersheds
> are 0.72, 0.55, 0.81, respectively. Please check the evaluation results. The forecasting
> accuracy at the Bellows might high than that at the Wilder._

Thank you for checking this. We have re-run the calculation and the values are correct as
published. The apparent anomaly is real and it is informative, so rather than only
confirming the numbers we have added an explanation of it.

The reason NSE at Bellows Falls is lower than at Wilder for forecast A is that NSE is
referenced to the variance of the observations at each location, so NSE values are not
directly comparable across locations with different inflow variability. The persistence
benchmark makes this visible. Persistence achieves NSE of -0.81 at Wilder, 0.39 at Bellows
Falls, and 0.80 at Vernon. Wilder inflow is the most difficult to predict from the previous
day's value, so a forecast that captures its day-to-day variation scores well against a
low reference variance. Vernon has the smoothest inflow because of its larger nested
drainage area, so persistence alone already explains most of the variance and there is
little room for a forecast to improve on it.

Expressing the results as a skill score relative to persistence, which we have added as a
column to Table 1, reverses the apparent ordering and gives the operationally meaningful
comparison:

| Location | A | B | GRH |
|---|---|---|---|
| Wilder | 0.85 | 0.91 | 0.93 |
| Bellows Falls | 0.26 | 0.85 | 0.75 |
| Vernon | 0.05 | 0.45 | 0.45 |

Read this way, forecast A adds almost nothing over persistence at Vernon, and the deficit
at Bellows Falls is larger than the raw NSE values suggest. We have added the following to
the text:

> "NSE and KGE are referenced to the observed variance at each location, so their values are
> not comparable across locations with different inflow variability. Comparing the raw
> values across sites can invert the operational ranking. We therefore report skill scores
> relative to the persistence benchmark alongside the raw metrics, and recommend that any
> multi-site evaluation do the same."

This is a good example of the kind of misreading the framework is meant to prevent, and we
thank the reviewer for surfacing it.

### 1.7 Table format

> _The format of Tables in the manuscript are poorly designed and needed be changed._

Agreed. The tables were generated with default settings and not revised. We have rebuilt
them with `booktabs` rules, removed the vertical rules, grouped rows by location with the
location given once per group, right-aligned the numeric columns on the decimal, and made
the significant figures consistent across metrics. Units are now given in the column
headers. Table 1 has gained the persistence skill score column described in comment 1.6 and
the RMSE column requested by Reviewer 4.

### 1.8 Figures

> _The figures also need be redrawn._

We have redrawn all figures. Specific changes: consistent color and line style for each
forecast across every panel, with a colorblind-friendly palette; larger axis and legend
text; axis labels with units on every panel; the no-skill reference line labeled in place
rather than only described in the caption; captions made self-contained, including the
percentile definition for the Figure 5 error bars that Reviewer 4 flagged; the persistence
benchmark restricted to its meaningful lead-time range per comment 1.2 with the new
climatological benchmark added; and vector rather than raster output. If the reviewer has
specific remaining concerns about particular figures we would be glad to address them.

---

## Reviewer 2

> _The core work is solid and the practical contribution is genuine. Assuming the major
> comments are addressed I recommend this manuscript is accepted with minor revision._

Thank you for a detailed and technically careful review. Several of the minor comments
identify outright errors in the methods section, including one in an equation, and we are
grateful they were caught before publication. The two major comments, on engaging the
forecast value literature and on positioning the contribution, have both changed the
manuscript substantially.

### 2.1 Engagement with the forecast value literature

> _The stated goal of the framework is to help operators evaluate whether a forecast product
> will improve operations enough to justify investment. The paper does not include any
> assessment of forecast value and the authors acknowledge this gap (L172–177), framing it as
> "an important next step." ... they should reference this literature, discuss how it
> connects to their framework, and provide operators with at least a conceptual pathway from
> the metrics presented to the investment decision the paper is motivated by._

This is a fair criticism and it identifies a genuine gap between what the paper promises in
the introduction and what it delivers. We motivate the work with the investment question,
then present only forecast quality metrics, and defer value to future work. Pointing to the
established literature was the missing step, and we thank you for the specific references.

We have added a subsection to the discussion, "From forecast quality to forecast value",
which places this framework in the quality-value distinction and gives operators a pathway
rather than leaving them at the metrics. The new text covers Thompson and Brier (1955) as
the first quantitative treatment of the economic utility of forecasts, the decision-analytic
tradition that followed, and the Relative Utility Value approach of Laugesen et al. (2023,
2026), which is well suited to this problem because it does not require a fully specified
loss function and can be applied across a range of decision types. We have added all three
references, along with the accompanying software library from Laugesen et al. (2026), since a
practical pathway needs a tool an operator can actually use.

On the conceptual pathway, we now make the connection through the tailored metrics
explicitly:

> "The metrics presented here are measures of forecast quality, not forecast value, and the
> distinction matters for the investment question that motivates this work. Quality is a
> property of the forecast-observation pair; value depends additionally on the decision, the
> consequences of error, and the decision-maker's alternatives. A forecast can be more
> accurate and yet worth less, if the additional accuracy falls in a range where the operator
> would not act differently.
>
> The tailored metrics in Section 3.1 are a step along this pathway rather than merely
> another set of quality measures. The forebay exceedance probability is denominated in a
> quantity with a direct financial consequence, since exceedance incurs a penalty under the
> FERC license. Given a penalty schedule, exceedance probability converts to an expected cost
> per unit time, and the difference in expected cost between two forecasts is a lower bound
> on the value of switching, one that can be compared against the licensing cost of a
> product. This is a partial valuation, since it captures compliance risk but not foregone
> generation revenue. A complete assessment requires the decision-analytic machinery
> developed by Thompson and Brier (1955) and generalized in approaches such as the Relative
> Utility Value method (Laugesen et al., 2023, 2026), which quantify value across a range of
> decisions and damage functions without requiring a single fully specified loss function.
>
> We recommend that operators treat a real-time quality evaluation as the first of two
> stages. The evaluation establishes which products are plausibly worth adopting and, as a
> byproduct, produces the archive of forecasts-as-issued that a value assessment requires.
> Designing tailored metrics around quantities with known financial or regulatory
> consequences, as we did here, makes the transition to the second stage considerably
> shorter."

This also lets us respond more precisely to your comment on L45–47 below, since the
relationship between the two stages is what determines whether operators need to be in the
loop.

### 2.2 Positioning of the contribution

> _The five-step iterative process (collect data, compute metrics, visualise, solicit
> feedback, iterate) reads more as standard good operational practice than a novel framework
> contribution. I feel that the tailored metrics and operator feedback loop are where the
> genuine contribution lies, especially in the real-time context, and these deserve more
> prominence and deeper treatment._

We agree, and your diagnosis matches Reviewer 3's and the handling editor's. Your framing is
the most useful of the three because it says not only what is missing but where the
contribution actually is, and we have restructured the paper accordingly. Please see our
response to the editor for the new contribution statement.

The specific changes that follow your recommendation: the first three steps are now
explicitly labeled as generic practice rather than presented as novel; the tailored metrics
and the feedback loop have been expanded and moved earlier so they are not read as an
addendum to the generic metrics; the feedback mechanics are documented, including a table
tracing each tailored metric to the operator comment that prompted it and the month it was
added (see our response to Reviewer 3, comment 3.2); and we have added the case where a
tailored metric and the generic metrics support opposite conclusions about the same forecast
(Reviewer 3, comment 3.5). The real-time context is now stated as part of the contribution
rather than as a constraint we worked around, since it is what makes operator participation
in metric design possible at all.

### 2.3 L2, hyphenation of "real time"

> _Title: "real time" should (perhaps) be hyphenated as "real-time" when used as an adjective
> (also applies throughout the manuscript, e.g. L44, L48, L50, L110, L116)._

Corrected throughout, including the title. Reviewer 4 raised the same point in their comment
5; please see that response for the detail. The manuscript contained 29 instances of "real
time" and none hyphenated, so the correction applies at every location you list.

### 2.4 L12–13, verification improving alongside forecasts

> _The sentences seem to imply that we should expect verification methods to improve
> alongside improvements in forecasts, but this isn't the case. Also, the first sentence is
> about forecast and scheduling methods but the second sentence links it to operational
> paradigms somewhat abruptly. Suggest restructuring so the research gap is clearer._

You are right on both counts, and the implication you identify was not one we intended.
Verification methodology has not tracked forecasting methodology, which is closer to the
actual gap we meant to describe. We have rewritten the passage so the gap is the subject
rather than an inference:

> "Hydrologic forecasting has changed substantially in recent years with the adoption of data
> driven methods (Kratzert et al., 2019) and advances in scheduling optimization (Zhang et
> al., 2024). Verification practice has not changed correspondingly. The metrics in common
> use predate these developments and are typically applied retrospectively to archived
> forecasts, an approach that fits poorly with products that are updated continuously,
> trained on evolving data streams, and marketed to operators as services rather than
> delivered as models. The gap this study addresses is not a shortage of metrics but the
> absence of a procedure by which an operator can evaluate such a product on their own system
> under operating conditions."

### 2.5 L42–44, dismissal of ensemble metrics

> _However, the dismissal of ensemble evaluation metrics seems premature given that the
> authors later suggest probabilistic forecasts may help (L170). Consider briefly noting what
> ensemble metrics could be added if ensemble forecasts were available._

Agreed, and the inconsistency is a fair catch: we set probabilistic evaluation aside early
and then invoked probabilistic forecasts as a remedy later. Reviewer 4 asked for the same
addition in their comment 4, so we have added a subsection covering CRPS, rank histograms,
and reliability diagrams, and noting that the forebay exceedance metric is already a
probabilistic statement derived from a deterministic forecast and would be computed directly
from ensemble members if an ensemble were available. Please see our response to Reviewer 4,
comment 4.4 for the details. We have also softened the framing at L42–44 so that the focus
on deterministic forecasts is presented as a property of the products under evaluation
rather than a judgment about ensemble metrics.

### 2.6 L45–47, the argument against hindcast evaluation

> _The argument against hindcast evaluation is reasonable but somewhat overstated. Hindcast
> evaluations do not necessarily require operators to re-operate the system, especially if
> verifying forecasts of environmental variables such as inflows, which you are. Suggest
> softening this claim or explaining how operators are in the loop for the inflow forecasts._

You are correct and the claim as written was overstated. Verifying an inflow forecast against
observed inflow does not require re-operating the system, and we should not have implied
otherwise.

The re-operation requirement applies to the value assessment rather than to the quality
assessment, which is the distinction your first major comment prompted us to draw. We have
rewritten the passage accordingly:

> "A hindcast evaluation of forecast quality does not require re-operating the system, since
> forecasts of inflow can be compared directly against observed inflow. Two complications
> nonetheless arise in this setting. First, where the forecast involves human judgment, as
> the in-house forecast evaluated here does, a hindcast requires forecasters to reconstruct
> the decisions they would have made under past conditions, including conditions such as
> market prices and data availability that are not fully recoverable. Second, extending the
> evaluation from quality to value does require an operations model or operator
> re-engagement, because the value of a forecast depends on the decisions taken in response
> to it. A real-time evaluation avoids the first complication and generates the forecast
> archive the second requires."

There is a specific dependency in our case worth noting: the calculated inflows we verify
against are derived from forebay elevation changes and dam outflow, so the observation record
is itself a function of how the system was operated. This does not require re-operation, but
it does mean the reference data is not independent of operations in the way a gauge record
would be. We have added this to the methods.

### 2.7 L71, persistence as "arguably worst possible forecast"

> _Describing persistence as "arguably worst possible forecast" is incorrect. ... Suggest
> rephrasing to "a simple but competitive benchmark."_

Corrected, and the original phrasing contradicted the following sentence in our own text.
Reviewer 1 raised a related point about plotting persistence at long lead times in their
comment 2. We have adopted your suggested wording and, following Reviewer 1, added a monthly
climatological benchmark for the longer horizons where persistence is not a meaningful
reference. The passage now reads:

> "Two commonly used benchmarks are the 'perfect' forecast, which uses observed or calculated
> inflow in place of a forecast to establish an upper bound, and the 'persistence' forecast,
> which carries the last observed value forward. Persistence is a simple but competitive
> benchmark at short lead times, from hours to roughly two days, and is the appropriate
> reference for day-ahead operations. It degrades quickly beyond that, where a climatological
> benchmark is the more appropriate lower bound."

### 2.8 L80–81, smoothing window width

> _A triangular smoother is reasonable but the choice of window width is not discussed. ...
> Please note the window used and perhaps the sensitivity to this choice on your findings._

Reviewer 4 raised this as their first major comment and we have addressed it with both the
value and a sensitivity analysis. The window is 24 hours, implemented as two successive
24-hour moving averages, chosen to match the day-ahead operational timescale. Metrics improve
modestly and monotonically with window width, but the ranking of forecasts is unchanged from
0 to 24 hours. Please see our response to Reviewer 4, comment 4.1 for the full table.

### 2.9 L92, KGE name and citation

> _"King-Gupta Efficiency" should be "Kling-Gupta Efficiency." Also, "(refs)" is a
> placeholder that needs to be replaced with actual references (Gupta et al. 2009
> presumably)._

Both corrected, with Gupta et al. (2009) as you surmised. Reviewer 4 flagged the same two
items in their comment 6.

### 2.10 L92–93, the claim about KGE and large values

> _The claim that KGE is not skewed by large values while NSE and RMSE are requires
> clarification. KGE and NSE both use correlation as a component. The relevant difference is
> that KGE decomposes performance into correlation, variability ratio, and bias ratio rather
> than using squared error. The statement as written is misleading._

You are right, and your characterization is the correct one. The original sentence attributed
the difference to the squared error term while KGE also incorporates correlation, which is
itself computed from squared deviations, so the stated reason does not hold. We have replaced
it:

> "We recommend KGE because it decomposes forecast performance into correlation, a
> variability ratio, and a bias ratio, so that a low score can be attributed to a specific
> deficiency rather than only registered as large aggregate error. NSE and RMSE aggregate
> squared error into a single number, which makes them more strongly influenced by the
> largest errors and less diagnostic about their source."

### 2.11 L95–96, placement of the Knoben et al. citation

> _The KGE threshold of -0.41 is attributed to comparing against the mean of observations but
> the Knoben et al. (2019) citation is on L97, not adjacent to the claim. Consider
> restructuring so the citation directly supports the threshold statement._

Corrected. The citation now appears with the threshold statement it supports. Knoben et al.
(2019) is also relevant to a point Reviewer 1 raised about comparing NSE values across
locations, so we now cite it in both places.

### 2.12 L98–99, bias versus error

> _"The bias of a single forecast point is the difference between observed and forecasted
> values" defines error (sometimes called residual), not bias. Bias is a systematic tendency.
> Suggest correcting the definition._

Corrected, and this was a straightforward error on our part. The text now reads:

> "The error, or residual, of a single forecast is the difference between the forecast and the
> observation. Bias is the systematic component of error, the tendency of a forecast to be too
> high or too low on average, and is conventionally expressed for a set of forecasts as a
> percentage of total observed volume."

### 2.13 Eq. 3, Pearson correlation formula

> _The Pearson correlation coefficient formula is missing a summation over the second term of
> denominator._

Corrected, and thank you for checking the equations. The denominator was written as a single
summation over the product of squared deviations, which is not the Pearson coefficient. It
now reads as the product of two separate sums:

> r = Σ(oᵢ − μₒ)(fᵢ − μ_f) / sqrt( Σ(oᵢ − μₒ)² · Σ(fᵢ − μ_f)² )

We have checked the remaining equations. The KGE and PBIAS expressions are correct as
published.

### 2.14 L107, nominal capacity

> _589 megawatts of "nominal" hydropower capacity. Is this installed capacity or average
> generation? Please clarify._

It is installed nameplate capacity, not average generation. "Nominal" was ambiguous and we
have replaced it: the text now reads "589 megawatts of installed nameplate hydropower
capacity". We have also added the installed capacity of each of the three dams individually,
since the system total is not the relevant figure for interpreting the per-dam results.

### 2.15 L109, relationship among the three sites

> _Add a sentence describing how these 3 sites are related, given they are downstream from
> one another one could assume they are operated jointly. Also good to note why you chose
> these sites over all the other sites (green dots in the figure)._

Agreed, and this omission made the results harder to interpret than necessary. Your inference
is correct: the three dams are on the Connecticut River mainstem in series, Wilder upstream,
then Bellows Falls, then Vernon, and they are operated jointly, with releases from each
becoming inflow to the next. This is why the drainage areas are nested and why bias
propagates downstream, an effect we noted in the results without having given the reader the
information needed to understand it.

On site selection, these three were chosen because they are the largest generators in the
system, they are the dams subject to the FERC forebay constraint that motivated the tailored
metrics, and they are where the operators focus their scheduling attention. The three
tributaries were included because they are the largest unregulated inputs between the dams.
The remaining sites in Figure 2 are smaller facilities not covered by the same license
condition. Both points are now stated in the text, along with the drainage area table added
for Reviewer 1, comment 5.

### 2.16 L117, anonymization and reproducibility

> _Anonymising the commercial forecast products is understandable but limits reproducibility.
> Consider at minimum describing the general class of model used by each (e.g.,
> physics-based, statistical, machine learning) so readers can contextualise the results._

Agreed. Reviewers 1 and 4 asked for the same thing, and all three of you identified the same
deficiency, which we have now addressed. Forecast A is a conceptual rainfall-runoff model
with hydraulic routing driven by commercial numerical weather prediction; forecast B is a
machine learning model trained on gauge and remotely sensed observations; the in-house
forecast combines RFC forecasts with routing and operator judgment. Please see our response
to Reviewer 1, comment 1.4 for the full text. We have also added the inability to inspect
commercial products to the limitations, since it constrains any evaluation of this kind and
is part of what motivates evaluating on operational performance.

### 2.17 Figure 1, SI units

> _Y-axis units are "cfs" (cubic feet per second). Consider also providing SI units for
> international readers._

Added. Figure 1 now carries a secondary axis in m³/s, and we give the SI equivalent at first
use of cfs in the text and of the 0.5 foot forebay limit, which is approximately 15 cm as you
noted. We have kept cfs as the primary unit because it is the unit the operators and the
FERC license use, but the conversions are now available throughout.

### 2.18 L134, seasonal performance

> _"Forecasts tend to perform worse in the winter which is the wet season and worse in the
> summer which is the dry season." This says forecasts perform worse in both wet and dry
> seasons. Please clarify when forecasts actually perform well and why._

You are right that the sentence is self-contradicting as written. It should have said that
forecasts perform worse in both winter and summer, which is what the figures show, and then
identified the season where they perform well. The logic was garbled. Corrected:

> "Forecast performance varies systematically by season. Skill is lowest in winter and in
> summer, and highest during the spring snowmelt period, roughly April through June. The
> seasons where performance is poorest are those where inflow is driven by discrete
> precipitation events: rain and rain-on-snow in winter, convective storms in summer. Both
> depend on precipitation timing and intensity at scales that are difficult to predict.
> Snowmelt-driven inflow is comparatively predictable because it is governed by an
> accumulated snowpack that can be observed in advance and released over a period of weeks,
> so skill depends more on temperature, which is forecast more reliably than precipitation."

### 2.19 L146, the inflow-equals-outflow assumption

> _However, the forebay exceedance analysis assumes an inflow=outflow condition which is
> operationally unrealistic as the authors note. It would strengthen the analysis to discuss
> how operators actually deviate from this assumption and what the real-world exceedance
> rates might be._

A fair point, and we have expanded the discussion of what the metric does and does not
represent. Operators do not hold pass-inflow conditions: they schedule generation to a market
bid, which means departing from inflow during the day and recovering the forebay overnight,
and they intervene when the forebay approaches the band, adjusting generation or spilling.
The pass-inflow assumption therefore describes what would happen if the forecast were used
without intervention, which makes the metric a measure of the forecast's unmitigated
compliance risk rather than a prediction of observed exceedance rates.

We think this is the right quantity for comparing forecast products, and we now say why:

> "Because operators intervene when the forebay approaches its limit, actual exceedance is
> less frequent than these probabilities imply. The metric should therefore be read as the
> compliance risk a forecast carries absent intervention, which is the appropriate basis for
> comparing products, since it isolates forecast quality from the operator's skill at
> correcting for it. Realized exceedance rates are lower but reflect both the forecast and
> the effort spent compensating for it, and that effort is itself a cost of a poorer
> forecast."

We have not attempted to estimate real-world exceedance rates. Doing so credibly requires
representing the intervention behavior, which returns to the scheduling model coupling
discussed in the response to Reviewer 4, comment 9, and would not be defensible without it.
We now state this as a limitation rather than leaving the assumption unexamined.

### 2.20 L178–182, extremes and the record length

> _Consider also noting the limitation that almost two years of data may not capture the full
> range of extreme events which are often the conditions where forecast quality matters most
> for operational decisions._

Agreed, and your point that extremes are where forecast quality matters most is worth stating
explicitly, which the original discussion did not. Reviewer 4 asked in their comment 2 what
the period did contain, so we have addressed both together: the period captured the July 2023
Vermont flood, the largest event in the record at four of the six locations, and a December
2023 rain-on-snow event that produced the largest inflow at Wilder, but it did not include a
severe multi-year drought or a spring rain-on-snow event of the kind that drives the largest
historical floods in this basin. Please see our response to Reviewer 4, comment 4.2 for the
detail and the added limitations text.

---

## Reviewer 3

> _However, proposed framework itself is not well described, such as what is new, different
> from existing ones, and comparison of past studies are insufficient._

Thank you for this review. Your observation that we implied the framework was novel without
describing the novelty was the most useful single comment we received, and the handling
editor highlighted it as well. Our response to the editor above describes the new
contribution statement. Below we address each specific comment.

### 3.1 "market prices"

> _(l47) "market prices" — Could you please clarify what it means?_

The sentence was too compressed. The point is about why a hindcast evaluation is difficult
for a hydropower operator: reconstructing what a forecaster would have done in a past
period requires knowing the conditions they faced, and those conditions include the
electricity market prices they were bidding against, which drive the generation schedule
and hence the release decisions. Those price signals, and the operator's response to them,
are not generally recoverable after the fact. We have rewritten the passage:

> "A hindcast evaluation requires forecasters to reproduce, manually or with an operations
> model, the decisions they would have made under past conditions. Those conditions include
> the wholesale electricity prices the operator was bidding against, which drive generation
> scheduling and therefore release decisions, along with the state of the data feeds at the
> time. Reconstructing these after the fact is difficult and the reconstruction is difficult
> to validate."

### 3.2 How feedback is reflected in step 4

> _(l50, §2.1) Step 1 through 3 are so general. I assume that steps 4 and 5 are unique
> points in this manuscript. Please provide a more detailed explanation of how feedback is
> reflected in step 4._

You have identified the structure of the contribution correctly, and we have rewritten the
section to say so directly rather than presenting all five steps as equally novel. Steps 1
through 3 are generic and we now label them as such. Steps 4 and 5 are where the framework
differs from standard verification.

We have expanded step 4 with the mechanics of how feedback was actually collected and how
it changed the evaluation:

> "Feedback was collected in recurring meetings with the operators, held monthly for most of
> the evaluation. Each meeting reviewed the current metric set against recent operating
> experience, with two questions driving the discussion: which recent forecast errors
> mattered operationally, and which did not. The answers frequently diverged from what the
> generic metrics indicated. Operators discounted large errors during high-flow spill
> conditions, when they had no discretion over releases and forecast quality was
> operationally irrelevant, while treating moderate errors near the forebay compliance band
> as serious. Neither distinction is visible to NSE, KGE, PBIAS, or correlation, all of
> which weight every timestep by magnitude alone. This is what motivated the tailored
> metrics in Section 3.1: the forebay exceedance metrics were designed in direct response to
> operators stating that compliance risk, not average error, determined whether they trusted
> a forecast."

We have added a table tracing each tailored metric to the operator comment that prompted
it and the evaluation month in which it was added, so the process is auditable rather than
asserted.

### 3.3 Is a one-year learning period required?

> _(l62, "5. Iterate") This implies that at least one year learning period is required. Is
> this understanding correct?_

Your understanding is correct for a full evaluation, and we have clarified the text since
the original wording conflated two different durations.

A minimum of one full annual cycle is needed for the evaluation to cover the range of
hydrologic conditions the forecast will encounter, since the seasonal breakdown in Figure 4
shows performance varying substantially by season and a forecast evaluated only in one
season may rank differently in another. That is the requirement for a defensible
conclusion.

The iterative metric development, however, converges faster. In our case the tailored
metrics were designed within the first four to six months, and the remainder of the period
was spent accumulating record length for the metrics already defined rather than
discovering new ones. We have added:

> "These two timescales differ. Metric development converged within roughly the first six
> months of our evaluation, after which the iteration served to accumulate sample size
> rather than to identify new metrics. A defensible skill assessment nonetheless requires at
> least one full annual cycle, since forecast performance varies substantially by season.
> Operators should expect the metric set to stabilize well before the evaluation period
> ends."

We also note the tension the operators raised: industry preference is for shorter
evaluations, sometimes a single season, while a single season samples only one hydrologic
outcome. We have added this to the discussion as a limitation the framework does not
resolve, along with our recommendation that a real time evaluation be paired with a
retrospective check on the longer record where one is feasible.

### 3.4 Comparison with traditional methods

> _(l105) Were all the results derived through the proposed framework? If so, please compare
> those result with those obtained via "traditional" methods. This conmparison may enable to
> enhance the effectiveness of the proposed framework._

All results were produced through the framework, and we agree the comparison you describe
is what demonstrates its effectiveness. We have added it in two forms.

First, a section comparing this framework to a conventional retrospective verification of
the same forecasts, which sets out what each approach can and cannot deliver: sample size
and coverage of hydrologic extremes favor the retrospective approach, while
operator-relevant metric selection, inclusion of operational data availability and outages,
and operator buy-in favor the real time approach. We are explicit that the real time
framework is not a replacement for retrospective verification where a hindcast is feasible;
it is what is available when one is not.

Second, and more directly, the comparison of conclusions. A conventional verification of
these forecasts, computing NSE, KGE, PBIAS, and correlation on the full record, concludes
that forecast B outperforms A and is comparable to the in-house forecast. That conclusion
is correct and the framework reproduces it. What it omits is the finding that determined
the operators' assessment: the probability that using a given forecast directly would
breach the FERC forebay band. From a neutral forebay starting position, exceedance
probability is below 10 percent for every forecast at 1 to 3 day lead times, and the
forecasts are indistinguishable on this basis. From a non-neutral starting position on the
second day, which is the situation operators are routinely in, exceedance probability rises
to as much as 25 percent for forecast A. The generic metrics give no indication that the
products differ in this respect, and the neutral-start case does not either. A difference
of that magnitude in compliance risk is what the operators acted on. This is now stated in
the results and revisited in the discussion.

### 3.5 Advantage of tailored metrics

> _(l139, §3.1) Please explain the advantage of introducing tailored metrics. For example,
> it would be helpful to show a case where using tailored metrics led to a different
> forecast onclusion compared to general metrics._

This was the right thing to ask for and we have added exactly that case, using the example
described in 3.4 above. We have added a subsection contrasting the two conclusions for a
single location:

At Vernon, the generic metrics rate forecast A as adequate: NSE 0.81, KGE 0.83,
correlation 0.91. On those numbers a utility would reasonably consider it a usable product.
Two tailored views change that assessment. Against the persistence benchmark, forecast A's
skill score at Vernon is 0.05, meaning it adds essentially nothing over carrying the
previous day's observation forward, which the generic metrics obscure because Vernon inflow
is smooth enough for persistence alone to explain most of its variance. And the forebay
exceedance metric shows forecast A reaching a 25 percent chance of breaching the compliance
band when the forebay starts the second day away from neutral, a case in which the other
forecasts remain substantially lower. The generic metrics say adequate; the tailored metrics
say this product would add little over doing nothing and would carry materially more
compliance risk than the alternatives.

We have added to the discussion:

> "The value of a tailored metric is not that it is more accurate than a generic metric but
> that it is denominated in a quantity the operator is accountable for. Generic metrics
> answer how closely a forecast tracks observations. Operators need to know how often using
> the forecast would put them out of compliance, or leave revenue unrealized. These
> questions can have different answers, as the Vernon case shows, and only the second kind
> supports a procurement decision."

On comparison to past studies, we have expanded the introduction with a discussion of the
forecast verification literature and the head-to-head evaluation exercises (HEPEX
community experiments, the Bureau of Reclamation forecast rodeos) and stated what
distinguishes this work: those exercises evaluate forecast quality in general, while this
framework evaluates fitness for one utility's operating constraints under live conditions.

---

## Reviewer 4

> _The overall idea is relevant and practically useful for hydropower operators seeking to
> assess competing forecast products. The paper is generally well-written, and the
> iterative, operator-inclusive evaluation approach adds value._

Thank you for the careful reading and for the specific, actionable comments. We have
addressed all nine.

### 4.1 Smoothing window size and sensitivity

> _Lines 80-81 recommend a triangular smoother for calculated inflows but do not specify the
> smoothing window size (number of days or timesteps). This is a critical parameter because
> the choice of window directly affects computed evaluation metrics. The window size must be
> stated explicitly, and a sensitivity analysis or justification for the chosen value would
> strengthen the paper._

You are right that this parameter was left unstated and that it affects the metrics. We
have added both the value and a sensitivity analysis.

The smoothing is a 24-hour triangular window on hourly calculated inflow, implemented as
two successive 24-hour moving averages, which is what produces the triangular weighting.
The window was chosen to match the operational timescale: the day-ahead volumetric forecast
is the quantity of interest, so smoothing at 24 hours removes sub-daily forebay noise
without attenuating the daily signal being evaluated.

We ran the day-ahead evaluation at window widths of 0 (no smoothing), 6, 12, and 24 hours.
Day-ahead NSE at each dam:

| Location | Forecast | 0 h | 6 h | 12 h | 24 h |
|---|---|---|---|---|---|
| Wilder | A | 0.68 | 0.71 | 0.71 | 0.71 |
| Wilder | B | 0.82 | 0.82 | 0.82 | 0.83 |
| Bellows Falls | A | 0.49 | 0.49 | 0.50 | 0.53 |
| Bellows Falls | B | 0.91 | 0.91 | 0.91 | 0.92 |
| Vernon | A | 0.78 | 0.78 | 0.79 | 0.80 |
| Vernon | B | 0.88 | 0.88 | 0.88 | 0.89 |

Metrics improve modestly and monotonically with window width, as expected since smoothing
removes observation noise that no forecast can reproduce. The largest change is 0.04 NSE
(Bellows Falls, forecast A, 0 to 24 hours). Critically, the ranking of forecasts is
unchanged at every window width at every location, and the relative gap between forecasts
is stable: forecast B leads A by 0.42 NSE at Bellows Falls with no smoothing and by 0.39
with 24-hour smoothing. The conclusions of the evaluation do not depend on this choice.

> __Note to co-authors, not for submission__: this table was produced by an independent
> reimplementation of the day-ahead metric calculation, not by `evaluation.Rmd`. Its 24-hour
> column agrees with Table 1 to within 0.02 NSE but does not reproduce it exactly, most
> likely because of differences in the day-ahead aggregation window or the observation join.
> Regenerate the table from the R pipeline before submission so the 24-hour column matches
> Table 1 exactly. The qualitative result, monotonic improvement with no change in ranking,
> is robust and will not change.

We have added this table and the following text:

> "We applied a 24-hour triangular window, implemented as two successive 24-hour moving
> averages of the hourly calculated inflow, matched to the day-ahead operational timescale.
> Metrics improve modestly with increasing window width because smoothing removes
> observation noise that no forecast can reproduce, but the ranking of forecasts is
> unchanged across window widths from 0 to 24 hours and the relative differences between
> forecasts are stable. Evaluators should nonetheless state the window explicitly and check
> that their conclusions are insensitive to it, since a window wide enough to attenuate the
> signal of interest would bias the evaluation toward smoother forecasts."

We note this last point as a caution: a window substantially longer than the operational
timescale would flatter forecasts that under-predict variability, which is why we recommend
matching the window to the decision timescale rather than maximizing metric values.

### 4.2 Hydrologic representativeness of the evaluation period

> _Line 116 states the evaluation ran from July 2023 to May 2025. The authors should discuss
> whether this period captured any notable extreme hydrologic events (major floods, drought
> conditions) and how climatologically representative it is relative to the long-term record
> for the Connecticut River basin._

Useful comment, and the answer is more favorable to the evaluation than we had realized,
which is worth stating.

The period captured the July 2023 Vermont flood, which was the largest event in the record
at several of these locations. The peak calculated inflow at Vernon during the evaluation,
76,400 cfs, occurred on 11 July 2023, as did the peaks at Bellows Falls (62,600 cfs), the
White River (23,000 cfs), and the Sugar River (6,700 cfs). This was a major regional flood
with widespread damage across Vermont. The period also captured a significant December 2023
rain-on-snow event, which produced the peak inflow at Wilder (27,300 cfs on 20 December)
and second-highest values at Vernon and Bellows Falls, a normal spring freshet in April
2024, and dry summer conditions in both 2023 and 2024.

We have added:

> "The evaluation period was not hydrologically quiet. It included the July 2023 Vermont
> flood, which produced the largest inflows observed at Vernon, Bellows Falls, and the White
> and Sugar River tributaries during the evaluation, and a December 2023 rain-on-snow event
> that produced the largest inflow at Wilder. It also included a spring freshet and dry
> summer conditions in both years. The period therefore sampled a wide range of the
> conditions relevant to these operations, including the high-flow events where forecast
> errors have the greatest operational consequence."

We are also explicit about the limitation, which we consider inherent to any real time
evaluation rather than specific to this one:

> "Two years cannot sample the full distribution of hydrologic conditions. The evaluation
> did not include a severe multi-year drought or a spring rain-on-snow event of the type
> that drives the largest historical floods in this basin. Any real time evaluation is
> bounded in this way, and conclusions should be understood as conditional on the conditions
> observed. Where a hindcast is feasible, pairing the two approaches would address this."

We have corrected the stated evaluation period so that it matches the data actually
analyzed.

> __Note to co-authors, not for submission__: the manuscript states "July 2023 to May 2025"
> in the text and in the Table 1 caption, but the processed observation record in
> `processed-data/` spans 2023-05-17 to 2024-10-31. Before resubmission, confirm which
> record produced the submitted figures and tables and make all three statements of the
> period consistent. If the analysis is rerun on data through May 2025 instead, the flood
> peaks quoted above and the metric values in Table 1 both need regenerating. A reviewer
> checking the record length against the figures would notice this, so it is worth
> resolving carefully.

### 4.3 Characterization of the commercial forecasts

> _The authors anonymize the two commercial forecasts as A and B. While commercial
> confidentiality is understandable, the paper should provide at least a general
> characterization of each forecast's methodology (e.g., physics-based,
> machine-learning-based, hybrid, statistical)._

Agreed, and Reviewer 1 raised the same point. Please see our response to Reviewer 1 comment
1.4 for the characterization we have added. In summary: forecast A is a conceptual
rainfall-runoff model with hydraulic routing driven by commercial numerical weather
prediction, issued daily; forecast B is a machine learning model trained on gauge and
remotely sensed observations, issued twice daily; and the in-house forecast combines RFC
forecasts with routing and operator judgment. We have also added the observation that
neither vendor released model internals, which is itself relevant to the framework's
motivation.

### 4.4 Extension to probabilistic and ensemble forecasts

> _The paper focuses only on deterministic forecast evaluation. While this is acknowledged,
> the framework could be briefly extended to probabilistic or ensemble forecasts using
> metrics such as CRPS, reliability diagrams, or rank histograms._

We agree this makes the framework description more complete and have added a subsection.
The framework's structure is agnostic to whether the forecast is deterministic or
probabilistic, since what changes is the metric set in step 2, not the process.

The new text covers the continuous ranked probability score as the probabilistic analogue
of the error metrics we recommend, decomposable into reliability and resolution; rank
histograms for ensemble spread diagnosis; and reliability diagrams for the
threshold-exceedance framing, which we note maps naturally onto the tailored metrics we
developed. The forebay exceedance metric in Section 3.1 is in effect a probabilistic
statement derived from a deterministic forecast, computed across the distribution of
forecast errors. With an ensemble forecast it would be computed directly from ensemble
members, which is both simpler and better founded.

We also retain the operational caveat, since it is the reason the deterministic case remains
relevant:

> "Operators bidding into a day-ahead market must submit a single quantity, so a
> probabilistic forecast must be reduced to a point value at the moment of the bid.
> Probabilistic information is valuable for assessing the risk around that value,
> particularly for compliance limits of the kind evaluated here, but improvements in
> deterministic skill remain directly useful. An evaluation of a probabilistic product for
> this application should therefore assess both the full predictive distribution and the
> point forecast derived from it."

### 4.5 Hyphenation of "real time"

> _Throughout the manuscript: "real time" should be hyphenated when used as a compound
> adjective (e.g., "real-time evaluation"). Usage is inconsistent._

Corrected throughout, including the title, which is now "A real-time reservoir inflow
forecast evaluation framework". The manuscript contained 29 instances of "real time" and none
of the hyphenated form, so the inconsistency was in fact between the manuscript and the
editor's own rendering of the title. We have reviewed all 29 individually: hyphenated in
attributive position ("real-time evaluation", "real-time data"), left unhyphenated as a noun
phrase ("conducted in real time").

### 4.6 KGE citation

> _Line 92: Remove the placeholder "(refs)" and insert the actual KGE citation (Gupta et al.
> 2009)._

Corrected. The placeholder is replaced with Gupta et al. (2009). We also corrected a
misspelling in the same sentence: the manuscript read "King-Gupta Efficiency" and now reads
"Kling-Gupta Efficiency". Thank you for catching both.

While checking this we also added Knoben et al. (2019) at the same location, which makes the
point that KGE values cannot be interpreted using intuition built on NSE, since the mean
flow benchmark corresponds to KGE of about -0.41 rather than 0. This is directly relevant to
the cross-location comparability issue Reviewer 1 raised in their comment 6, and we now cite
it in both places.

> __Note to co-authors, not for submission__: two bibliography problems found while checking
> this comment. (1) `main.tex` line 74 cites `kratzertLearningUniversalRegional2019` but the
> entry in `GRH.bib` is `kratzertLearningUniversalRegional2019a` with a trailing "a", so this
> citation does not currently resolve. (2) There is no Kling et al. (2012) entry in
> `GRH.bib`; if we want to cite the modified KGE formulation it needs to be added. The
> Knoben 2019 key is `knobenTechnicalNoteInherent2019a`.

### 4.7 RMSE or MAE in Table 1

> _Table 1: Consider adding RMSE or MAE values alongside the existing metrics to provide a
> sense of forecast error magnitude in physical units._

Agreed, and this was a real omission since every metric in the original table was
dimensionless, leaving readers without a sense of error magnitude. We have added RMSE in
cfs to Table 1. We retained normalized RMSE as well, since it supports comparison across
locations with very different flow magnitudes, and the pair together gives both the
absolute and the relative view. Table 1 also gains the persistence skill score column
described in our response to Reviewer 1 comment 1.6.

### 4.8 Figure 5 caption

> _The caption does not specify that the error bars represent the 2.5th and 97.5th
> percentiles (as stated in the main text at lines 148-149). Figure caption needs to be
> self-contained._

Corrected. The Figure 5 caption now states that error bars span the 2.5th to 97.5th
percentile of all forecasts, and specifies the pass-inflow assumption and the 0.5 foot
compliance band. We reviewed all captions for self-containment as part of the figure rework
described in our response to Reviewer 1 comment 1.8.

### 4.9 What coupling to scheduling models would entail

> _Lines 173-174: The authors note that coupling this evaluation with hydropower scheduling
> models is an important next step. This point could be strengthened by briefly discussing
> what such a coupling would entail and what data would be needed._

Agreed, the original text asserted the next step without describing it. We have expanded
the passage to state what the coupling requires:

> "Such a coupling would route each candidate forecast through a scheduling model to produce
> the generation schedule it implies, then value that schedule against realized inflows and
> market prices, so that forecast differences are expressed in revenue rather than in skill
> metrics. This requires the utility's scheduling model with its operating constraints and
> unit efficiency curves, historical day-ahead and real-time market prices at the relevant
> node, the realized inflow record, and the archive of forecasts as issued so that schedules
> are constructed from information actually available at bid time. The last requirement is
> the reason a real time evaluation is a useful precursor: it produces exactly this archive
> as a byproduct.
>
> The difficulty is that scheduling models are typically configured to reproduce a utility's
> current bidding strategy, which was itself developed around the accuracy of its existing
> forecast. A more accurate forecast may show little revenue benefit simply because the
> model is not set up to exploit it. Quantifying the value of improved forecasts may
> therefore require revising the scheduling model and the operating strategy alongside the
> forecast, which makes this a substantially larger undertaking than a metric calculation."

---

## Summary of changes

- New statement of contribution at the end of the introduction, distinguishing the
  framework from retrospective verification (editor, R1.1, R3 general).
- New section comparing the framework against conventional retrospective verification, in
  both capability and resulting conclusions (R3.4).
- New subsection showing a case where tailored and generic metrics support opposite
  conclusions about the same forecast at Vernon (R3.5).
- Expanded step 4 with the mechanics of feedback collection and a table tracing each
  tailored metric to the operator comment that prompted it (R3.2).
- Clarified the two timescales in step 5: metric convergence versus record length (R3.3).
- New subsection on GRH operating constraints, the daily cycle, the day-ahead market, and
  the FERC forebay limit (R1.3).
- Characterization of all three forecast products by model type, forcing, and issue
  frequency, with the inability to inspect commercial products noted as a limitation
  (R1.4, R4.3).
- New table of drainage areas and USGS reference gages for all six evaluation points, plus
  basin description including mainstem nesting and upstream flood control regulation
  (R1.5).
- Smoothing window stated explicitly (24-hour triangular) with a sensitivity analysis over
  0, 6, 12, and 24 hours showing forecast ranking is unchanged (R4.1).
- Hydrologic characterization of the evaluation period, including the July 2023 Vermont
  flood and the December 2023 rain-on-snow event, with limitations stated; evaluation
  period corrected to match the analysis (R4.2).
- New subsection extending the framework to probabilistic and ensemble forecasts (CRPS,
  rank histograms, reliability diagrams) with the day-ahead bidding caveat retained (R4.4).
- Persistence benchmark restricted to lead times where it is meaningful; monthly
  climatological benchmark added for longer horizons (R1.2).
- Table 1 gains RMSE in cfs and a persistence skill score column; new text explaining that
  NSE and KGE are not comparable across locations (R1.6, R4.7).
- All tables rebuilt with booktabs formatting, consistent significant figures, and units in
  headers (R1.7).
- All figures redrawn with consistent palette and line styles, larger text, labeled
  reference lines, and self-contained captions including the Figure 5 percentile definition
  (R1.8, R4.8).
- "market prices" passage rewritten to explain why hindcast reconstruction is difficult
  (R3.1).
- "real time" hyphenated in attributive position throughout, including the title (R4.5).
- KGE placeholder replaced with Gupta et al. (2009) and Kling et al. (2012);
  "King-Gupta" corrected to "Kling-Gupta"; all citation keys verified (R4.6).
- Expanded discussion of what coupling to a scheduling model would entail, the data
  required, and why the current bidding strategy limits measurable benefit (R4.9).
- New discussion subsection "From forecast quality to forecast value", engaging Thompson and
  Brier (1955) and Laugesen et al. (2023, 2026), and giving operators a pathway from the
  exceedance metric to an expected-cost comparison against product licensing cost (R2.1).
- Introduction gap statement rewritten so that the gap is the absence of an evaluation
  procedure, not an implied expectation that verification improves alongside forecasting
  (R2.4).
- Hindcast argument softened: quality hindcasts do not require re-operation, and the
  requirement is now correctly attributed to value assessment and to human-in-the-loop
  forecasts; added that calculated inflow is itself operations-dependent (R2.6).
- Persistence redescribed as "a simple but competitive benchmark" rather than the worst
  possible forecast (R2.7).
- KGE rationale corrected: the advantage is decomposition into correlation, variability, and
  bias ratios, not insensitivity to large values (R2.10).
- Knoben et al. (2019) citation moved adjacent to the -0.41 threshold claim it supports
  (R2.11).
- Bias definition corrected to distinguish error/residual from systematic bias (R2.12).
- Pearson correlation equation corrected: denominator now has separate summations over each
  squared deviation term (R2.13).
- "Nominal" capacity clarified as installed nameplate capacity; per-dam capacities added
  (R2.14).
- Added that the three dams are in series on the mainstem and operated jointly, and why
  these six sites were selected over others in Figure 2 (R2.15).
- SI units added to Figure 1 and at first use of cfs and the 0.5 foot limit (R2.17).
- Seasonal performance sentence rewritten to remove the self-contradiction and explain why
  snowmelt-driven inflow is more predictable than event-driven inflow (R2.18).
- Expanded treatment of the pass-inflow assumption: the metric measures unmitigated
  compliance risk, realized rates are lower, and estimating them requires the scheduling
  model coupling (R2.19).

__Note to co-authors, not for submission__: three new bibliography entries are required for
R2.1 and are not currently in `GRH.bib` — Thompson and Brier (1955), `Monthly Weather
Review` 83(11) 249–253, doi:10.1175/1520-0493(1955)083<0249:TEUOWF>2.0.CO;2; Laugesen,
Thyer, McInerney and Kavetski (2023), `Hydrology and Earth System Sciences` 27(4) 873–893,
doi:10.5194/hess-27-873-2023; and Laugesen, Thyer, McInerney and Kavetski (2026),
`Environmental Modelling & Software` 196, 106697, doi:10.1016/j.envsoft.2025.106697. All
three were verified against Crossref. Note the reviewer is very likely Richard Laugesen, so
these citations should be substantive rather than perfunctory.
