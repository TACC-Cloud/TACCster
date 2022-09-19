Introduction to the Jupyter Notebook Environment 
===


Jupyter is an open source project that provides a webapp interface for writing code and documents. Throughout this tutorial, we will be using a Jupyter Notebook environment for accessing Tapis services. 

## Running Jupyter notebooks using Google Co-lab 

Step 1: You will login to [Google Colab](https://colab.research.google.com) with your google account.

Step 2: Once you login successfully, you should be presented with a dialog and you can select the Github tab and paste in the following URL https://github.com/TACC-Cloud/TACCster.git and then hit the search icon.

Step 3: You will then be shown a list of files, you can select img_classify.ipynb file and the the far button on the left (Open notebook in new tab).

Step 4: Now you need to install the Tapis Python SDK aka Tapipy in colab. Run the first code cell

!pip install tapipy 

Step 5: After running the above code you need to restart the runtime - go to the Menu and select Runtime -> Restart runtime or use CTRL+M on the keyboard. Now you can execute rest of the code in the notebook and follow the tutorial.

