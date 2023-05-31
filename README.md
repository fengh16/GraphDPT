# GraphDPT: Graph Distillation with Personalized Temperature for Large Scale Graph Data

## Environment

We use a conda environment. Please refer to `environment.yml`.

## Download the teacher knowledge

Use the following command to download teacher knowledge from Google Drive into `./distilled`.

```bash
python download_teacher_knowledge.py --data_name=<dataset>
```

## Reproduce the results

Run the following command in the root directory of this project. Please change the `--data_dir` and `--kd_dir` to your own path.


### Cora、CiteSeer、PubMed、Flickr、Reddit

Please run the code in `stu-gcn` directory. For example,

``` bash
cd stu-gcn && CUDA_VISIBLE_DEVICES=0 python train.py --dataset cora --dropout=0.1 --lr=0.001 --n-epochs=600  --n-hidden=64 --n-runs=10 --KD_alpha=9 --KD_CL_weight=20 --KD_CL_temp=1 --KD_CL_sample_num=10 --KD_attention_temp_smooth_addition_new_weight=1.0 --role=KD --KD_attention_temp_range_min 0.1 --KD_attention_temp_range_max 100 --data_dir /f/code/dataset/ --kd_dir /f/code/GraphDPT/distilled/
cd stu-gcn && CUDA_VISIBLE_DEVICES=1 python train.py --dataset citeseer --dropout=0.1 --lr=0.01 --n-epochs=1000 --n-hidden=256 --n-runs=10 --KD_alpha=10 --KD_CL_weight=10 --KD_CL_temp=0.8 --KD_CL_sample_num=10 --KD_attention_temp_smooth_addition_new_weight=0.5 --role=KD --KD_attention_temp_range_min 0.1 --KD_attention_temp_range_max 100 --data_dir /f/code/dataset/ --kd_dir /f/code/GraphDPT/distilled/
cd stu-gcn && CUDA_VISIBLE_DEVICES=2 python train.py --dataset pubmed --dropout=0.1 --lr=0.001 --n-epochs=600 --n-hidden=256 --n-runs=10 --KD_alpha=10 --KD_CL_weight=40 --KD_CL_temp=0.8 --KD_CL_sample_num=10 --KD_attention_temp_smooth_addition_new_weight=0.1 --role=KD --KD_attention_temp_range_min 0.1 --KD_attention_temp_range_max 100 --data_dir /f/code/dataset/ --kd_dir /f/code/GraphDPT/distilled/
```

### Arxiv、Yelp、Products

Please run the code in `stu-cluster-gcn` directory. For example,

``` bash
cd stu-cluster-gcn && CUDA_VISIBLE_DEVICES=3 python train.py -d=ogbn-arxiv --n-runs=10 --n-epochs=2000 --use-labels --use-linear --lr=0.01 --n-hidden=256 --dropout=0.1 --num_partitions=200 --batch-size=32 --KD_alpha=1 --KD_CL_weight=1  --KD_CL_temp=0.8 --KD_CL_sample_num=10 --role=KD --KD_attention_temp_range_min 0.1 --KD_attention_temp_range_max 100 --data_dir /f/code/dataset/ --kd_dir /f/code/GraphDPT/distilled/
cd stu-cluster-gcn && CUDA_VISIBLE_DEVICES=4 python train.py -d=ogbn-products --n-runs=2 --n-epochs=400 --lr=0.005 --n-hidden=512 --dropout=0.1 --num_partitions=160 --batch-size=4 --KD_alpha=1 --KD_CL_weight=0.5 --KD_CL_temp=0.8 --KD_CL_sample_num=10 --role=KD --KD_attention_temp_range_min 0.1 --KD_attention_temp_range_max 100 --data_dir /f/code/dataset/ --kd_dir /f/code/GraphDPT/distilled/
```
