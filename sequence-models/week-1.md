- Named entity recognition is used by search engines to index key words in articles so it is easy for users to search.
- You can't (not very effectively anyway) use a standard neural network model for identifying names because sometimes the output is of different length to the input e.g. get a list of all the names from a sentence and secondly, it doesn't share features learned across different positions of text.
- A one hot vector means the vector only has one 1, the rest are 0s. The opposite is a one cold vector.
- Choosing a good architecture to use can help reduce the number of parameters to train.
- A recurrent neural network tries to predict Y<i> using X<i> but it also uses some information from earlier step(s). The parameters that are used on each time step are shared.
- One weakness of RNNs is that it can only use information from an earlier sequence.
- Activation function is usually tanh and sometimes relu. Output is dependent on what you want the neural network to do e.g. sigmoid for binary classification or softmax if you have multiple categories.
- RNNs have a slightly different model compared to your standard neural network or CNNs. A<t> = g(WaaA<t-1> + WaxX<t> + Ba) and Y hat <t> = g(Wya A<t> + by)
- At each time step t, you take a<t-1>, x<t>, Wa and ba to calculate a<t>. This is used with your activation function, Wy and by to calculate Y hat <t>. Using Y hat <t>, you calculate the cost function loss<t>. Sum all the losses together and you get the overall loss function loss.
- Sampling means to generate something e.g. a sentence with your trained RNN model using something like np.random.choice.
- Instead of building your model using words, you can use characters as well. Using characters allows you handle unknown words but the disadvantage is that it is not as good as word based models at capturing the dependency on the earlier parts of a sentence on the later part of the sentence. Basically the sentences that character based models generate are all very long with each word having many characters.
- RNNs also have a similar problem with exploding / vanishing gradients. Exploding gradients can be somewhat addressed with gradient clipping (and also easier to spot since your values will overflow) but vanishing gradients are a little harder to deal with.
- Gated recurrent unit (GRU) helps to capture long range dependencies much better and helps with the vanishing gradients problem. GRU has 4 vectors:
1. To remember the original value (c)
2. To calculate the possible candidate value to update (c tilda)
3. To decide if the values should be updated (gamma u)
4. To decide how relevant the previous c<t-1> is for computing c tilda <t> (gamma r)
- Long short term memory (LSTM) is a more complex alternative to the GRU. LSTM has 5 vectors:
1. To remember the original value (c)
2. To calculate the possible candidate value to update (c tilda)
3. To decide if the values should be updated (gamma u)
4. To decide if the values should be forgotten (gamma f)
5. To decide the output (gamma o)
- Bidirectional RNNs (BRNNs) allow you to also use information from the future since the network is designed like an acyclic graph. 
- Deep RNNs are very expensive because of the temporal component in each individual layer.