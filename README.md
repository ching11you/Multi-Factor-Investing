How to run the code?
1. Dataset reqpuired contains returns/signals of your factor of interest and all assets in your market of interest.
2. Modify gt and rt variables in the code to redefine it to reflect your factor of interest.
3. Run the rest of the code as it is to obtain the results.

Methedology of the tool is provided below for further clarity with regards to the code.

Methodology
SPCA: a method that iteratively selects informative test assets, estimates principal components (factors), and projects out explained variation.

Step 1: Defining the target factor (“Supervised” component)
Pick a target factor to trade eg. cross-sectional momentum.

Step 2: Selection (Supervised Screening)
Identify most informative test assets by:

For each asset:

Regress its returns on the target factor
Compute the correlation or R² between the asset return and the target factor
Keep only the top assets with the highest absolute correlations (typically 30–50 assets)

Step 3: Estimation (PCA)
Apply PCA on the selected subset of test assets.
The first principal component extracted is treated as a latent factor most related to the target.
Step 4: Projection
Remove the influence of the estimated latent factor by projecting it out from both the target factor and all test asset returns. (This isolates what is still unexplained, preparing the data for the next iteration.)

Step 5: Iterate
Repeat Steps 2–4 on the residuals (unexplained part).
Each iteration captures a new latent factor relevant to the target.
Repeat p times — where p is chosen based on validation or performance metrics. (We performed a graphical illustration of the changes in explained variation at each iteration in our example code.)
Step 6: Risk Premium Estimation

  
Regress the original target factor on the extracted p latent factors.
This provides a consistent estimate of the target factor's risk premium, even when weak or latent factors are present in the data. (We performed a Fama MacBeth regression to calculate this.)
