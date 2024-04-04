## Auto MLFlow
An opensource automated MLOps library for MLFlow in python.

#### Github Repository: [Click Here](https://github.com/mr-ravin/auto_mlflow)

### Installation
- Install MLFlow.
  ```
  pip3 install mlflow
  ```
- Install Auto MLFlow.
  ```
  pip3 install auto_mlflow
  ```

#### Working Demonstration:
- Start a MLFlow Server.
  ```  
  mlflow server --host 127.0.0.1 --port 5555
  ```
- Use Auto MLFlow to log model and experiment related information.
  ```python
  import auto_mlflow
  user_name = "Ravin Kumar"
  project_name = "Object Detection"
  experiment_name = "Using Yolo approach"
  runName = "using yolov3"
  total_epochs = 30
  mlflow_server_uri = "http://127.0.0.1:5555" # IP address of the MLFlow Server.
  
  # initialisation 
  auto_mlflow.init_run(user_name, project_name, experiment_name, runName, mlflow_server_uri) # project, experiment, and run is created
  
  # below this line, whatever is printed in the terminal will also get logged in the MLFlow inside the file log.txt
  auto_mlflow.write_param(param_dict={"learning_rate": "0.001", "total_epochs": str(total_epochs)}) # save training related information
  
  # storing train, val, and test loss values
  model_architecture = get_model_architecture()
  for epoch in range(total_epochs):
    train_loss = ...
    valid_loss = ...
    test_loss = ...
    metric_dict={"train_loss": train_loss, "valid_loss": valid_loss, "test_loss": test_loss}
    auto_mlflow.write_metric(metric_dict, step = epoch)
  
  # storing an image in MLFlow Server
  numpy_array_bgr = visualised_image(.....)
  auto_mlflow.write_image(numpy_array_bgr, image_name="image.jpg")
  
  # storing text in a file inside MLFlow Server
  auto_mlflow.write_text(filename="additional_file.txt", filedata="object detection model")
  
  # storing already existing local file inside MLFlow Server
  # example- incase one wants to save only weights, and not rely on model registry. This will get saved inside weights/ in MLFlow Sever
  auto_mlflow.write_files("yolo_weights.pth", filepath="weights")
  
  # storing an entire directory present in local system, to the MLFlow Server
  auto_mlflow.write_directory("./other_data", mlflow_dir_path="artifacts") # this will copy all the content of ./other_data to MLFlow inside artifacts/
  
  # Logging a model
  auto_mlflow.log_model(model_architecture, model_run_path="models") # the logged model can be used for model registry
  
  auto_mlflow.end_run() # all the information is successfully saved.
  # complete 
  ```

LICENSE
```
Copyright (c) 2024 Ravin Kumar
Website: https://mr-ravin.github.io

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation 
files (the “Software”), to deal in the Software without restriction, including without limitation the rights to use, copy, 
modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the 
Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the 
Software.

THE SOFTWARE IS PROVIDED “AS IS”, WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE 
WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR 
COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, 
ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
```
