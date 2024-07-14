# ASSIGNMENT: Sampling and Reproducibility in Python

Read the blog post [Contact tracing can give a biased sample of COVID-19 cases](https://andrewwhitby.com/2020/11/24/contact-tracing-biased/) by Andrew Whitby to understand the context and motivation behind the simulation model we will be examining.

Examine the code in `whitby_covid_tracing.py`. Identify all stages at which sampling is occurring in the model. Describe in words the sampling procedure, referencing the functions used, sample size, sampling frame, any underlying distributions involved, and how these relate to the procedure outlined in the blog post.

Run the Python script file called whitby_covid_tracing.py as is and compare the results to the graphs in the original blog post. Does this code appear to reproduce the graphs from the original blog post?

Modify the number of repetitions in the simulation to 1000 (from the original 50000). Run the script multiple times and observe the outputted graphs. Comment on the reproducibility of the results.

Alter the code so that it is reproducible. Describe the changes you made to the code and how they affected the reproducibility of the script file. The output does not need to match Whitby’s original blogpost/graphs, it just needs to produce the same output when run multiple times

# Author: Abigeal A.

```
## Question 1: Identify all stages at which sampling is occurring

## Breakdown

1. Initialization and Constants
Constants:
ATTACK_RATE = 0.10
TRACE_SUCCESS = 0.20 (20%).
SECONDARY_TRACE_THRESHOLD = 2
individuals needed to trigger secondary tracing.

2. Simulation Function (simulate_event)
i. Event Creation
Sampling Frame: A DataFrame (ppl) representing 1000 individuals attending two types of events: 'wedding' (200 individuals) and 'brunch' (800 individuals).
Population Size: 1000 individuals.

ii. Infection Sampling
Function Used: np.random.choice
Procedure: Randomly selects 10% of the population to be infected based on the ATTACK_RATE.
Sample Size: int(1000×0.10)=100 individuals.

iii. Primary Contact Tracing Sampling
Function Used: np.random.rand
Procedure: For the infected individuals, a random value is generated, and if it's less than TRACE_SUCCESS (20%), the individual is marked as traced.
Sample Size: Depends on the number of infected individuals (approximately 100).

iv. Secondary Contact Tracing Sampling
Procedure: If the number of traced individuals at an event meets or exceeds SECONDARY_TRACE_THRESHOLD, all infected individuals at that event are marked as traced.
Sampling Frame: Events with at least 2 traced individuals.
Sample Size: Varies based on the number of such events and infected individuals at these events.

v. Calculating Proportions
Procedure: Calculates the proportion of infections and traced cases attributed to weddings vs. brunches

3. Simulation Repetition and Bootstrapping
Function Used: List comprehension with simulate_event(m) for m in range(1000)
Procedure: Runs the simulation 1000 times to generate a distribution of the proportion of infections and traces attributed to 'weddings'.
Sample Size: 1000 repetitions

4.  Plotting Results
Procedure: Uses seaborn's histplot to plot histograms of the bootstrapped proportions.
Sample Size: 1000 bootstrapped samples for each of the proportions.
  
## Question 2: Does this code appear to reproduce the graphs from the original blog post?

- No. The graph looks different from the one in the blog post.

## Question 3: Comment on the reproducibility of the results.
- Without a seed or similar setting, the outputted graphs vary each time when running the script because it lacks reproducibility.

## Question 4: Describe the changes you made to the code and how they affected the reproducibility of the script file.

- First is to set a seed for random number generation. Second is to save the results of random sampling to disk and generated plots using the same data from disk each time. These two ways would achieve the same reproducibility of the plots.




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
