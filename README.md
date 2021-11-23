<h1 align="center">Determining stock price direction by using CNN on 1-D time series data encoded as 2-D Images</h1>

<p>
    In this project, we have made an attempt to predict the direction of the close and mid-price of a stock using
    2D-CNNs by converting a 1-D time series regression
    problem into a 2-D image classification problem. We have explored and compared various techniques that can be
    utilized to achieve the aforementioned task along with
    all the challenges that we faced in the way.
</p>

<h2>Stock Dataset</h2>

<p>
    This project makes use of <a href="https://www.kaggle.com/satnam007/bajajcombined" target="_blank">Bajaj Finance
        daily stock prices</a> dataset from Kaggle.
    This dataset spanning from the year 2003 to the year 2020 contains open, high, low and close prices of the company’s
    stock as well as its total volume traded.
</p>

<h2>Overview</h2>

<p align="center">
    <img src="/readMeAssets/proposed_methodology.png" alt="Proposed Methodology" width="80%" />
</p>

<p>Our purpose was to try to predict the direction of close and mid prices of this dataset.
<ul>
    <li>
        We started by labelling all the samples as "Buy", "Hold" and "Sell" for both close
        and mid prices. To do this, we used 2 different labelling strategies in each case.
    </li>
    <li>
        We started by creating 3 dataframes with different engineered features:
        <ul>
            <li>
                <strong>TA_NORMALIZED_DATA: </strong>
                For this data frame, we used the open, high, low, close and volume values from the original dataset and
                fed them as arguments to a function in python
                Technical Analysis(TA) Library to get a wide range of technical indicators. Then all the values were
                rescaled in the range of unsigned integers
                from 0 to 255.
            </li>
            <li>
                <strong>PCA_NORMALIZED_DATA: </strong>
                A linear kernel was employed with PCA on the normalized technical indicators returned by the TA library
                to get a data frame with reduced dimensionality which
                was then combined with the original normalized data frame value.
            </li>
            <li>
                <strong>30_BEST_TA_NORMALIZED_DATA: </strong>
                The K best feature selection strategy was applied on the calculated technical indicators returned by the
                TA library to select 30 features that contributed the
                most towards the target variable.
            </li>
        </ul>
    </li>
    <li>
        We then prepared three types of images for each combination of three data frames (<strong>TA_NORMALIZED_DATA,
        PCA_NORMALIZED_DATA, 30_K_BEST_TA_NORMALIZED_DATA</strong>), two labelling
        strategies (<strong>Labelling Strategy 1, Labelling Strategy 2</strong>) and price types (<strong>mid-price, close price</strong>). Those three
        types are mentioned below:
        <p align="center">
            <img src="/readMeAssets/image_type.PNG" width = "70%"/>
        </p>
    </li>
    <li>
      The prepared datasets were split into 80:20 ratio and saved on drive. We ended up with the following folder structure:
      <p align = "center">
        <img src="/readMeAssets/outer_folder_structure.JPG" width = "30%"/>
        <img src="/readMeAssets/inner_folder_structure.JPG" width = "20%"/>
        <img src="/readMeAssets/image_folder_structure.JPG" width = "20%"/>
      </p>
    </li>
    <li>
        The images were then 
        trained and evaluated on 3 different architectures of 2D CNN to 
        accommodate all possible scenarios of overfitting and 
        underfitting. The three architectures here are referred to as 
        CNN_4 (ARCH1), CNN_6(ARCH2) and CNN_8(ARCH3). 
        All the architecture configurations are detailed in the figures 
        below. Apart from the already discussed max pooling and batch 
        normalization layers, there’s also a dropout layer employed in 
        CNN_8 and CNN_6 with a dropout ratio of 0.4 to ensure 
        minimal overfitting. All three architectures had a learning rate 
        of 0.001, used adam optimizer which is the industry standard 
        for multi-class classification, sparse categorical cross-entropy 
        as the loss function and ReLU as the activation function.
        All the models were trained for 5 and 10 epochs. Each time, the 
        stride values for one of the layers was changed from two to 
        three. For evaluation, we used the accuracy and F1 metrics.
        <p align = "center">
          <img src="/readMeAssets/CNN_arch_1.png" width = "40%"/>
          <img src="/readMeAssets/CNN_arch_2.png" width = "40%"/>
        </p align = "center">
        <p>
          <img src="/readMeAssets/CNN_arch_3.png" width = "90%"/>
        </p>
    </li>
</ul>
</p>

<h2>Results, Conclusion and more</h2>
<p>
   In order to get insights on result and conclusion, as well as to get a thorough understanding of what we did,
   check out our full <a href="/projectReport.pdf">project report pdf</a> in the repository.
</p>
