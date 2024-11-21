# ASSIGNMENT: Sampling and Reproducibility in Python

Read the blog post [Contact tracing can give a biased sample of COVID-19 cases](https://andrewwhitby.com/2020/11/24/contact-tracing-biased/) by Andrew Whitby to understand the context and motivation behind the simulation model we will be examining.

Examine the code in `whitby_covid_tracing.py`. Identify all stages at which sampling is occurring in the model. Describe in words the sampling procedure, referencing the functions used, sample size, sampling frame, any underlying distributions involved, and how these relate to the procedure outlined in the blog post.

Run the Python script file called whitby_covid_tracing.py as is and compare the results to the graphs in the original blog post. Does this code appear to reproduce the graphs from the original blog post?

Modify the number of repetitions in the simulation to 1000 (from the original 50000). Run the script multiple times and observe the outputted graphs. Comment on the reproducibility of the results.

Alter the code so that it is reproducible. Describe the changes you made to the code and how they affected the reproducibility of the script file. The output does not need to match Whitby’s original blogpost/graphs, it just needs to produce the same output when run multiple times

# Author: YOUR NAME

```
1. Initial Setup and Sampling Frame

Events Setup: 200 entries for "wedding" and 800 entries for "brunch" are created, simulating a scenario where there are a total of 1000 individuals split across these two event types.

Data Frame Creation: A DataFrame is created with columns for 'event', 'infected', and 'traced' status, initialized to False for 'infected' and NaN for 'traced'.


2. Infecting Individuals

Sampling for Infections:

Function Used: numpy.random.choice()

Sample Size: int(len(ppl) * ATTACK_RATE), which calculates to 10% of 1000, i.e., 100 individuals.

Sampling Frame: The index of the DataFrame ppl, representing all individuals.

Underlying Distribution: Uniform random selection without replacement, meaning each individual has an equal chance of being selected without the possibility of being selected more than once.

This randomly selects indices from the DataFrame to simulate the individuals who get infected.



3. Primary Contact Tracing

Sampling for Tracing:

Function Used: numpy.random.rand()

Sample Size: Number of infected individuals, dynamically determined by sum(ppl['infected']).

Sampling Frame: Infected individuals.

Underlying Distribution: Uniform distribution between 0 and 1. A person is marked as traced if a generated value is less than TRACE_SUCCESS (20% chance).

This process simulates random success in tracing infected individuals, based on the tracing success rate.



4. Secondary Contact Tracing

Threshold-Based Tracing:

Procedure: Counts of traced individuals are aggregated by event type. If the count of traced individuals in an event type reaches the SECONDARY_TRACE_THRESHOLD of 2, then all infected individuals at those events are also marked as traced.

This simulates a scenario where discovering multiple cases at an event triggers a broader tracing response, potentially identifying additional cases through secondary contact tracing.



5. Aggregation and Calculation

The simulation calculates proportions of infections and traces attributed to weddings compared to brunches, using basic conditional filtering and aggregation techniques within the DataFrame.


6. Repetition and Analysis

Monte Carlo Simulation: The simulate_event function is run 50,000 times, creating a large sample of results from the simulated model.

Analysis: Results are stored in a DataFrame and visualized using histograms to compare the distribution of infections and traced cases attributed to weddings.

Question 2:

Comparing both graphs, they are difference in them in various ways, the labelling of the X and Y axis are different, what the histogram represent are different also.

The Python script did not reproduce the exact graph from the original blog post, there are differences:

Overlay vs. Separate: The first graph overlays the histograms, making it difficult to distinguish between the true and observed proportions unless focusing on areas where one colour dominates. The second graph separates them, clearly delineating the differences in distribution and central tendency.

Distribution Shape: The second graph shows a marked difference in the distribution shapes, with the observed proportions spread over a wider range than the true proportions. This difference implies a bias introduced by the contact tracing method, likely overstating the role of weddings in spreading infections.

Central Tendency: The true proportion histogram (blue) in the second graph is more narrowly centred, suggesting a consistent true proportion of cases from weddings across simulations. The observed proportion (red) histogram suggests a variability and possible overestimation in how many cases are thought to be traced back to weddings, likely due to the method of contact tracing which may prioritize or be more efficient at identifying certain types of exposures.

Comments on the reproducibility of the graphs when I ran it multiple times by modifying the number of repetitions in the simulation to 1000 from 50000:

Consistency in Distribution: Both graphs show a very similar distribution of results, indicating good reproducibility of the simulation results. The shapes of the histograms in both graphs suggest that the underlying stochastic model generates consistent outcomes when repeated.

Reproducibility of Trends: The specific trends, such as the overestimation of traced cases at higher proportions compared to actual infections, are consistently reproduced in both graphs. This reproducibility is essential for validating the simulation model's reliability and for trusting its implications.

Quantitative Matching: Both graphs quantitatively match in terms of the ranges of proportions and the frequencies at which these proportions occur. This consistency further supports the reliability of the simulation setup and execution.

Finally, the histograms confirms that the results are reproducible, showing consistent distribution shapes, trends, and quantitative outcomes across multiple runs of the simulation. This consistency indicates that the model's setup, including its random number generation and sampling methods, is stable and reliably reproduces the same patterns of results under the same conditions.

I added "np.random.seed(42)" in the code and this ensures that the random processes always produce the same result each time the scripts run. It is achieved by setting the random seed before any operation that relies on randomness.





```


## Criteria

|Criteria|Complete|Incomplete|
|--------|----|----|
|Altercation of the code|The code changes made, made it reproducible.|The code is still not reproducible.|
|Description of changes|The author explained the reasonings for the changes made well.|The author did not explain the reasonings for the changes made well.|

## Submission Information

🚨 **Please review our [Assignment Submission Guide](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md)** 🚨 for detailed instructions on how to format, branch, and submit your work. Following these guidelines is crucial for your submissions to be evaluated correctly.

### Submission Parameters:
* Submission Due Date: `HH:MM AM/PM - DD/MM/YYYY`
* The branch name for your repo should be: `sampling-and-reproducibility`
* What to submit for this assignment:
    * This markdown file (sampling_and_reproducibility.md) should be populated.
    * The `whitby_covid_tracing.py` should be changed.
* What the pull request link should look like for this assignment: `https://github.com/<your_github_username>/sampling/pull/<pr_id>`
    * Open a private window in your browser. Copy and paste the link to your pull request into the address bar. Make sure you can see your pull request properly. This helps the technical facilitator and learning support staff review your submission easily.

Checklist:
- [ ] Create a branch called `sampling-and-reproducibility`.
- [ ] Ensure that the repository is public.
- [ ] Review [the PR description guidelines](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md#guidelines-for-pull-request-descriptions) and adhere to them.
- [ ] Verify that the link is accessible in a private browser window.

If you encounter any difficulties or have questions, please don't hesitate to reach out to our team via our Slack at `#cohort-3-help`. Our Technical Facilitators and Learning Support staff are here to help you navigate any challenges.
