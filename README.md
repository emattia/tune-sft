## Setup 

1. Install Python 3.12
2. `pip install -r dev-reqs.txt`

## Manual run

### Download a model using torchtune

[Read more](https://pytorch.org/torchtune/stable/tutorials/first_finetune_tutorial.html#downloading-a-model).
```bash
tune download meta-llama/Llama-3.3-70B-Instruct --output_dir $BASE_MODEL_DIR
```

### SFT

Check out the [`70B_sft_config.yaml`](./70B_sft_config.yaml) file and corresponding [`full_sft_distributed.py`](./full_sft_distributed.py).
These files work together to drive the torchtune fine-tuning process.
Here we run them independent of Metaflow to highlight the separation of concerns.

```bash
tune run --nproc_per_node 8 full_sft_distributed.py --config 70B_sft_config.yaml 
```

The config file has a parameter called `output_dir`. 
This determines where the tuned model weights are saved to disk. 

### Metaflow

```bash
python flow.py run
```