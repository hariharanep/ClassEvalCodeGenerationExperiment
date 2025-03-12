# ClassEvalCodeGenerationExperiment

These are the configurations for my local machine where I was able to slightly modify and execute the ClassEval benchmark code provided in this link: https://github.com/FudanSELab/ClassEval <br />
<img width="481" alt="Screenshot 2025-03-11 at 4 44 30 AM" src="https://github.com/user-attachments/assets/cfe0aaa6-1357-4e3b-98c1-172621f19297" /> <br />
I'm also using version 3.8.18 which is the preferred Python version to use for everything to work. To replicate the experiment that occurred in the ClassEval paper, I first had to execute the following commands in the terminal to make sure I had all the required Python packages installed. <br />
<br />
pip install -r requirements.txt
<br />
pip install torch torchvision torchaudio
<br />
pip install -U sentence-transformers
<br />
<br />
I evaluated the GPT-4 and GPT-3.5 LLMs in two different ways for this experiment. First, I evaluated these LLMs on the ClassEval benchmark with the following configurations: LLM temperature of 0.2, nucleus sampling strategy where the number of samples generated is 3, and a holistic code generation strategy. In order to execute this evaluation I had to cd into the generation folder and execute this command through the terminal: <br /><br />

python inference.py \
--model <9 for GPT-4 and 8 for GPT-3.5> \
--openai_key <providehere> \
--output_path ../output/model_output/model_output.json \
--greedy 0 \
--sample 3 \
--data_path ../data/ClassEval_data.json \
--generation_strategy 0 \
--openai_base https://api.openai.com/v1
<br /><br />

After the inference.py Python code finished executing, I had to cd into the classeval_evaluation folder and execute this command through the terminal: <br /> <br /> 
python evaluation.py --greedy 0
<br /><br />
Once this command finished executing, I was able to see the json files containing the pass@k results, the individual test case results, and the model output results in the output folder.
<br /><br />
For the second part of my experiment, I evaluated the GPT-4 and GPT-3.5 LLMs under all 3 code generation strategies in the ClassEval benchmark with the following configurations: LLM temperature of 0.2, greedy decoding strategy where the LLM only generates one sample. In order to execute this evaluation I had to cd into the generation folder and execute this command through the terminal: <br /><br />
python inference.py \
--model <9 for GPT-4 and 8 for GPT-3.5> \
--openai_key <providehere> \
--output_path ../output/model_output/model_output.json \
--greedy 1 \
--data_path ../data/ClassEval_data.json \
--generation_strategy <0 for holistic generation strategy, 1 for incremental generation strategy, 2 for compositional generation strategy> \
--openai_base https://api.openai.com/v1
<br /><br />
After the inference.py Python code finished executing, I had to cd into the classeval_evaluation folder and execute this command through the terminal: 
<br /><br />
python evaluation.py --greedy 1
<br /><br />
Once this command finished executing, I was able to see the json files containing the pass@k results, the individual test case results, and the model output results in the output folder.
