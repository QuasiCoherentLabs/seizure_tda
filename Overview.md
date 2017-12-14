# Timeseries TDA

## Project ideas:

- (1) Use `Seiz`, with the NN + TDA classification methods
- (2) Downsampling method for timeseries utilizing Betti Numbers
- (3) Blogpost applying FinTimeSeries approach to Crypto-currency
- (4) Topo signal proc applied to `Seiz`, brain as manifold, sheafify signals

### Interest level:
Scale from [1,5] _(5 is highest)_:
_(B,E)_
- 4,5
- 5,4
- 5,4
- 3,3

### Challenge level:
Scale from [1,5] _(5 is highest)_:
_(B,E)_
- 4,3
- 3,4
- 3,2.5
- 5,5

### Prioritize
In some sense, the previous numbers combine with pay-off to generate a prioritization list:
- (E) 3,1,2,4
- (B) 1,3,2,4

## Glossary

- `Seiz`: Seizure data set

## (1) NN + TDA on `Seiz`:

- Notebook on Qcoh Github for Seiz data
- Notebook on Eric's Github for TSTDA

- 24 1hr obs per patient, 25ish patients, 25 nodes per hour, 256 vals per sec ~13.5B

### What is TSTDA

- Take timeseries, with a collection of it's rolling windows of length `n` in this case let `n=20`
- Assume a dimensionality for embedding, in this case `RR^2`
- Then each rolling window consists of 20 values, which yield 19 points in `RR^2` by consecutive pairs of function values from the original timeseries, contained in this rolling window (Euclidean metric).
  - `X = (t_i, x_i)...`
  - `X_RW_1 = (t_0, x_0)...(t_19,x_19)`
  - `X_RW_1^Emb = [(x_0,x_1), (x_1,x_2)...(x_18,x_19)]`
- Then vary the radius from 0-infty(discretized) to compute persistant homology
- Betti numbers are computed at each discrete radius, for each homology degree (matrix)
- Betti_sum is the sum of all elements in the matrix

### Idea behind the Betti_matrix+NN paper

- Used a collection of movement TS, with labelings
- Doesn't use rolling windows, he embeds into `RR^3` using consecutive triples on the entire series,
- Computes Betti_matrix (3 cols)
- Feeds these matrices into CNN trained on matrices
  - Features are the `3xm` values inside these matrices where `m` is the number of epsilons
- Uses this to classify TS, good performance vs. traditional methods of TS classification

### application of Betti_matrix+NN to `Seiz`

- Label rolling windows with `contains seizure` binary
- Use above method to classify windows with these labels

### Questions

- What about only one epsilon sum per series?
- What about only one betti number per series?
- What are the papers involved in this idea? (Betti_sum and chaos, Betti_matrix and NN, TDA and `Seiz`)
- There's a relationship between subsets of the same TS, should we use the entire TS to normalize?
- Add patient and series_id as features and see if this improves performance?
- Use aggregate values in the matrix to feed in to the CNN?
- Compare to RF for classification?

### To-do

- (E) Understand how to build the CNN
- (B) Some data eng around slicing the series into their windows and randomizing
- Pull the TSTDA work into the same repo as the `Seiz`
  - (B) pipelining the windows into Betti matrices
- (B) consider the data size and what that necessitates
- (B) Build framework for the above other questions to be analyzed
- build RF classifier for these data


