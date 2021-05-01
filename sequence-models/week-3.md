- Language modelling is very similar to that of machine translation. Essentially all you have to do is replace the input with a representation of the input. For example, if it's an image then you want to use a CNN which contains a feature vector of all the features (which is a representation of the imagei) as an input. You could even use some kind of encoder to understand words in a different language. Everything else (decoding network RNN) remains the same.
- Machine translation is different from language modelling in that you don't sample randomly because otherwise sometimes your translation is correct, sometimes it's off / wrong. What you want to do is to try and maximize the probability of a string of translated text (Y hat) given an input X. The most common algorithm for this is beam search.
- You can't use a greedy algorithm (picking the word with the highest probability) because you might end up with a sub optimal translation.
- Since the search space is so huge e.g. if your translated output has 10 words and each word can is 1 from a possible vocab of 10000 words, that's 10000^10, you need to use some approximate search function.
- Beam width = number of possibilities that the beam algorithm considers at a time and it keeps track of these words in memory.
- The algorithm tries to find the second word based on the input X and the first predicted word, the third word based on the input X, the first and second words etc.
- Step 2 of beam algorithm takes the top 3 (beam width) of the most likely pairs (3 * 10000 pairs)
- Step 3 of the beam algorithm takes the 3 words kept in step 2 (so pairs of words) and repeat the algorithm to find the top 3 triplets.
- Running time of beam search is 3*10000 * 10 words. If b = 1, it is a greedy search algorithm.
- The larger the beam width is, the more accurate your translation but also the more computationally expensive.
- Beam search is not guaranteed to find the maximum value.
- You can compare y hat with y (human translation) to do error analysis. If P(y) > p(y hat), the fault is w/ beam search because it's returning a less optimal sentence. If P(y hat) >= P(y) then maybe the RNN model is at fault since y is supposed to be the correct output.
- Once you've done an error analysis on a sample of sentences, you can figure out which component (RNN or beam search) is responsible for more errors.
- A problem with the current design is that the encoder decoder model tries to encode the ENTIRE sentence and tries to output an appropriate translation. Performance of this degrades the longer your sentence! How humans naturally translate sentences are in parts which is what the attention model does.