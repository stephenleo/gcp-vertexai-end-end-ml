# gender prediction
## LSTM to predict Gender based on US names dateset

This repo has been reworked from the ground-up to use GCP Vertex AI Training and Model Serving of a tensorflow LSTM model. The model has been trained on ~30K names stored in sharded tfrecords and can be distributed using tensorflow MultiWorkerMirroredStrategy. Test data accuracy is pending.

## Testing the latest GCP AI platform published API:
1. Create a JSON file with the names of interest with similar structure as below
    ```
    {"instances":[{"name":"stephen"}, {"name":"stephanie"}]}
    ```

2. Update the path to your json file in `testing/online_predict.sh`
    ```
    -d @path_to_your_json_file.json
    ```

3. Run online_predict.sh
    ```
    cd testing
    sh online_predict.sh
    ```

4. Output is a JSON object
    ```
    {'predictions': {'probability': [0.9067956805229187, 0.5227343440055847], 'gender': ['M', 'F']}}
    ```

## Training data is from: 
Table name: `bigquery-public-data.usa_names.usa_1910_current`
Data Query: [Notebook](notebooks/00_DataQuery.ipynb)

## Training the model on GCP AI platform:
1. Update the parameters in `training/config_base.yaml`. Especially the model save path
    ```
    - msp="gs://leo-us-name-gender/model/x/"
    ```

2. Run train.sh
    ```
    cd training
    sh train.sh
    ```

You can view the progress of your training on [GCP Vertex AI console](https://console.cloud.google.com/vertex-ai/training/custom-jobs?project=leo-gcp-sanbox)

## Publishing a Serving API to GCP AI Platform:
To be updated
