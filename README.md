
<body>
    <h1>AN2DL Challenge 2 - Time Series Forecasting</h1>
    <h2>Introduction</h2>
    <p>The goal of this project was to design and implement forecasting models to predict future values in time series based on past observations. The provided dataset's actual meaning was unknown, consisting of 48,000 independent monovariate time series from six different domains.</p>
    <p>For extensive information about the task: <a href="https://codalab.lisn.upsaclay.fr/competitions/16514" target="_blank">AN2DL Challenge 2 competition page</a>.</p>
    <h2>Data Analysis and Input Preparation</h2>
    <p>The dataset included time series of varying lengths (from 24 to 2776). Approximately 99% of the sequences had a length below 650. The time series were already normalized in the range [0,1]. After cleaning duplicates, we tried two different strategies for sequence preparation. The best-performing model used the first strategy, which involved deleting time series with lengths outside a predefined range to speed up training.</p>
    <h2>Models Implemented</h2>
    <h3>LSTM</h3>
    <p>We started with a standard LSTM model, which performed decently, but adding complexity (e.g., more layers and bi-directionality) resulted in worse performance and overfitting.</p>
    <h3>ResNet</h3>
    <p>Based on a suggestion from our TA, we adapted a ResNet model for time series forecasting, which slightly improved performance over the LSTM.</p>
    <h3>Encode-Decode LSTM</h3>
    <p>This model improved over the ResNet. The model consists of an encoder that reads the input sequence and a decoder that makes one-step predictions based on the encoded input.</p>
    <h3>GRU and Bi-GRU</h3>
    <p>We tested the GRU model, which has fewer parameters than LSTM. It performed better than LSTM on our dataset, possibly due to the limited amount of training data. However, adding bi-directionality worsened the performance.</p>
    <h3>GRU Attention</h3>
    <p>We experimented with adding an attention layer before the GRU decoder. While the model performed well, it did not surpass the basic GRU model.</p>
    <h3>GRU Autoregression</h3>
    <p>We also tested a GRU model with autoregression. Although it performed well for single-step predictions, accuracy decreased when predicting multiple values in sequence.</p>
    <h2>Final Model and Hyperparameter Tuning</h2>
    <p>Our final model was a GRU with the following hyperparameters:</p>
    <ul>
        <li><strong>Window:</strong> 50</li>
        <li><strong>Stride:</strong> 5</li>
        <li><strong>GRU Units:</strong> 128</li>
        <li><strong>Dropout Rate:</strong> 0.2</li>
        <li><strong>Batch Size:</strong> 256</li>
        <li><strong>Epochs:</strong> 30</li>
        <li><strong>Early Stopping Patience:</strong> 6</li>
        <li><strong>Learning Rate (Reduce on Plateau):</strong> Patience 4, Factor 0.1, Min LR 1e-5</li>
    </ul>
    <h2>Conclusion</h2>
    <p>In the second phase of the competition, our GRU model achieved the following results:</p>
    <ul>
        <li><strong>MSE:</strong> 0.00931830</li>
        <li><strong>MAE:</strong> 0.06643198</li>
    </ul>
    <p>This final model was used similarly to an autoregression model, predicting twice and adjusting the input between predictions. Despite trying different models, the GRU remained the best performer throughout the competition.</p>
    <h3>Contribution</h3>
    <p>All team members contributed to various stages of the project, from data analysis to model implementation and fine-tuning.</p>
    <p><strong>Authors:</strong> Francesco Colabene, Andrea Gerosa, Christian Lisi, Giulio Saulle</p>
</body>
</html>
