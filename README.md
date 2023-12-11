# EvoGen-Prompt-Evolution but with Turbo
![Evolved Prompt Output](/Media/banner.png "Evolved Prompt Output")
## Description & Method
EvoGen is an evolutionary algorithm that optimizes prompts for text-to-image models for aesthetics, as assessed by @rivershavewings aesthetics model. 
The notebook is based on [https://github.com/MagnusPetersen/EvoGen-Prompt-Evolution] by Magnus Petersen.

I added SDXL-Turbo and LCM support for LCM-Dreamshaper-v7, and switched it back to GPU Generation - the originial works on TPU and JaxDiffusion which was unfortunately abandoned by Colab. 

### Hyperparameters
#### Evolutionary Algorithm Settings

General population settings, such as how many generations the algorithm runs for, how many prompts there are in each generation, and the word length range of the prompts.

* **generations:** How many generations the algorithm runs for.

* **population_count:** How many prompts there are in each generation/how large each generation is.

* **prompt_length_max:** Maximum prompt length when the population is initialized, during evolution this limit can be surpassed.

* **prompt_length_min:** Minimum prompt length when the population is initialized, during evolution this limit can be surpassed.

* **artist_prop:** Probability to sample from the artist list when adding or mutating a word.

* **genre_prop:** Probability to sample from the genre list when adding or mutating a word.

* **custom_prop:** Probability to sample from the custom user-defined list when adding or mutating a word.

The difference between the sum of the three custom lists and 1 is the probability to sample from the English dictionary word list.

* **require_custom_words:** If it is set to "True" the custom list will not just serve as a list to sample from but it will be required that each prompt in the population has min_custom_words words from the list in it. 

* **min_custom_words:** The number of words from the custom list required to be in the prompt.

* **use_aes_words:** Replaces the English dictionary that is the basis of the prompt generation with a curated word list derived from prompts with aethetics ratings 5 or higher from the simulacra aesthetics dataset. The base aesthetics score will be higher but I find the generations to be less interesting.

* **use_aes_engrams:** Replaces the English dictionary that is the basis of the prompt generation with a curated 2- and 3. gram list derived from prompts with aethetics ratings 5 or higher from the simulacra aesthetics dataset. If use_aes_words and use_aes_engrams are ticked both lists are concatinated.

* **delete_prop:** probability to delete a word per word in each prompt after each generation.

* **add_prop:** probability to add a new word per word in each prompt after each generation from the word lists.

* **mutate_prop:** probability to swap out a word per word in each prompt after each generation for a new word from the word lists.

* **shuffle_prop:** The probability to shuffle the order of words per prompt.

* **cross_prop:** The cross-over probability is the probability of the parents of the next generation swapping prompt parts per parent pair.

* **k:** K denotes the rounds in the tournament selection process. A higher K value means fewer parents generate the next generation, this means a higher score increase but less diversity in the prompts.

* **cutoff:** Cutoff aesthetics score to save and display the image and prompt.

* **use_prompt:** True if you want to guide the evolution with an additional prompt and not just aesthetics.

* **use_image:** True if you want to guide the evolution with an additional image prompt and not just aesthetics.

* **prompt_weigth:** The weight of prompt & image prompt. For instance 0.6 means the score is the result of 60% prompt+image prompt and 40% aesthetics.

#### Image Generation Settings
Image generation settings have an impact on the speed and behavior of the evolutionary algorithm, the euler_a sampler in conjunction with low step size and resolution is advisable for quick prompt evolution. Good prompts can then later be used to generate higher-quality images.

* **num_inference_steps:** The number of denoising steps. A higher step number will increase image quality but take longer to generate.

## To Do
* **Hyperparameter Tuning:** The hyperparameters are barely tuned and there is a lot of performance to be had when it comes to aesthetics optimization, prompt diversity, and optimization speed. 

* **Evolutionary Algorithm Tuning:** The algorithm is very basic and I have not read much on evolutionary algorithms. Here there is still a lot of room for improvement. Especially the crossover stage of the algorithm might be suboptimal the way it is done now for text.

* **General Features:** There are some features I would like to add, especially having a "base" prompt that is in each population member so that you can take your favorite prompt and build on it.
