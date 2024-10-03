## EXNO-3-DS

# AIM:
To read the given data and perform Feature Encoding and Transformation process and save the data to a file.

# ALGORITHM:
STEP 1:Read the given Data.</br>
STEP 2:Clean the Data Set using Data Cleaning Process.</br>
STEP 3:Apply Feature Encoding for the feature in the data set.</br>
STEP 4:Apply Feature Transformation for the feature in the data set.</br>
STEP 5:Save the data to the file.v

# FEATURE ENCODING:
1. Ordinal Encoding
An ordinal encoding involves mapping each unique label to an integer value. This type of encoding is really only appropriate if there is a known relationship between the categories. This relationship does exist for some of the variables in our dataset, and ideally, this should be harnessed when preparing the data.
2. Label Encoding
Label encoding is a simple and straight forward approach. This converts each value in a categorical column into a numerical value. Each value in a categorical column is called Label.
3. Binary Encoding
Binary encoding converts a category into binary digits. Each binary digit creates one feature column. If there are n unique categories, then binary encoding results in the only log(base 2)ⁿ features.
4. One Hot Encoding
We use this categorical data encoding technique when the features are nominal(do not have any order). In one hot encoding, for each level of a categorical feature, we create a new variable. Each category is mapped with a binary variable containing either 0 or 1. Here, 0 represents the absence, and 1 represents the presence of that category.

# Methods Used for Data Transformation:
  # 1. FUNCTION TRANSFORMATION
• Log Transformation
• Reciprocal Transformation
• Square Root Transformation
• Square Transformation
  # 2. POWER TRANSFORMATION
• Boxcox method
• Yeojohnson method

# CODING AND OUTPUT:
```
Developed by:RUDESH KANNA R</br>
Register No: 24900303</br>
```
import matplotlib.pyplot as plt</br>
import seaborn as sns</br>
import statsmodels.api as sm</br>
import scipy.stats as stats</br>
import numpy as np</br>
```
df = pd.read_csv("Encoding_data.csv")</br>
```
df.head()</br>
![372034180-3c4708b7-1e8e-404f-bfa4-ad9828da4d8b](https://github.com/user-attachments/assets/8340e4b7-de53-4d89-94da-d4a0c15bdaa1)</br>
```
df.tail()</br>
![373125493-69993b8c-66db-4689-8250-a37230bbcbae](https://github.com/user-attachments/assets/3269ed51-c52c-4ead-830b-ed33ef1ee7ed)</br>
```
df.describe()</br>
![372034567-b470ef07-1cd5-4484-b711-9f61520d7e56](https://github.com/user-attachments/assets/c9b33baa-7b6f-479b-8bde-25024764c4e7)</br>
```
df.info()</br>
![372034715-b0a38927-ebd6-4b90-abd7-5b21436f8901](https://github.com/user-attachments/assets/06033e1e-418c-4241-be85-e075e0393151)</br>
```
df.shape</br>
![373125662-576d78f3-6747-422a-9a3f-31b79b218db7](https://github.com/user-attachments/assets/b590a19f-2179-45f5-bc69-f22b7d5559db)</br>
```
df</br>
![373126577-f62c2a51-ccd7-4888-bd01-1e29443f765f](https://github.com/user-attachments/assets/643adb4a-7531-479c-82eb-0e3ee3f93b45)</br>
```
ordinal encoder</br>
from sklearn.preprocessing import LabelEncoder, OrdinalEncoder</br>
pm=['Hot', 'Warm','Cold']</br>
oe=OrdinalEncoder(categories=[pm])</br>
oe.fit_transform(df[["ord_2"]])</br>
![373126198-af3fcacf-b7eb-457e-98d9-3889b41d7e2a](https://github.com/user-attachments/assets/435bc90a-af61-40d8-8bff-09ecfcf5a1bc)</br>
```
df['bo2']=oe.fit_transform(df[["ord_2"]])</br>
df</br>
![372035445-f4824aa3-72e2-4354-b39a-14d7bc6c5da8](https://github.com/user-attachments/assets/d4f18880-0e42-40a2-b381-e99caa627d60)</br>
```
label Encoder</br>
le=LabelEncoder()</br>
dfc=df.copy()</br>
dfc['ord_2']=le.fit_transform(dfc['ord_2'])</br>
dfc</br>
![372035614-43d81ec8-49ab-43ef-888b-d7f097a39452](https://github.com/user-attachments/assets/fe96f9e7-5700-4c7c-9a7f-72fdcbc04fbb)</br>
```
One hot encoder</br>
from sklearn.preprocessing import OneHotEncoder</br>
ohe = OneHotEncoder(sparse = False)</br>
df2=df.copy()</br>
enc=pd.DataFrame(ohe.fit_transform(df2[["nom_0"]]))</br>
df2=pd.concat([df2,enc],axis=1)</br>
df2</br>
![372035923-b1ddad21-90b8-4159-9548-8eca78a7dae5](https://github.com/user-attachments/assets/69c725d7-154f-47b1-b69c-2cede5f387ad)</br>
```
pd.get_dummies(df2,columns=["nom_0"])</br>
![372036143-a0ea2434-a534-4afa-8b91-b17617c06e5a](https://github.com/user-attachments/assets/c57b52a6-30ba-49f6-be40-f813e553107d)</br>
```
pip install --upgrade category_encoders</br>
from category_encoders import BinaryEncoder</br>
df= pd.read_csv("data.csv")</br>
df</br>
![372036425-421dc1e1-fcb5-4202-87da-4517a20956d6](https://github.com/user-attachments/assets/7ee8d4f0-e6a4-4c1d-ba79-d10e62c9dde4)</br>
```
binary encoder</br>
be = BinaryEncoder()</br>
nd=be.fit_transform(df['Ord_2'])</br>
dfb=pd.concat([df,nd],axis=1)</br>
dfb1=df.copy()</br>
dfb</br>
![372036654-9f44b784-9b99-41d2-8f29-39d3693cbbae](https://github.com/user-attachments/assets/c52d18cc-d9a3-42d9-b413-8e7d5f18f142)</br>
```
target encoder</br>
from category_encoders import TargetEncoder</br>
te=TargetEncoder()</br>
cc=df.copy()</br>
new = te.fit_transform(X=cc["City"],y=cc["Target"])</br>
cc=pd.concat([cc,new],axis=1)</br>
cc</br>
![image](https://github.com/user-attachments/assets/a21804ba-05dd-4de3-9c60-a8a5fcb935a4)</br>
```
Feature Transformation</br>
import pandas as pd</br>
from scipy import stats</br>
df=pd.read_csv("Data_to_Transform.csv")</br>
df</br>
![372037136-3b1ec929-ad0e-47fb-b39a-03d9c228d6e1](https://github.com/user-attachments/assets/86b94325-435d-480e-a3ac-b3bb8e67201f)</br>
```
df.info()</br>
![372037288-327ed0d1-2f8f-41c5-9da9-125c79d5d1ff](https://github.com/user-attachments/assets/262408e0-45a4-499f-b361-8e97ab51166b)</br>
```
df.describe()</br>
![372037451-5f5c8f7a-49be-48dc-86c1-400a0214618d](https://github.com/user-attachments/assets/cb9f4fc5-5f25-42e6-891a-5ece85d16675)</br>
```
df.size</br>
![372037588-4af8996e-d807-4ba2-8def-1ddcddca8d4d](https://github.com/user-attachments/assets/21be224b-8502-4753-8ad7-b8b6d2d18b00)</br>
```
df.skew()</br>
![372037729-8be208a6-db9f-4d23-abb3-7ccd8661225a](https://github.com/user-attachments/assets/f840ce9d-f0dc-4fb5-8b76-9e59813c70e9)</br>
```
np.log(df["Highly Positive Skew"])</br>
![372037918-78aafe8a-29e8-4602-94cf-04d5a6412c76](https://github.com/user-attachments/assets/13094b10-864f-46fa-ae91-83e81ff9bdce)</br>
```
np.reciprocal(df["Moderate Positive Skew"])</br>
![372038134-11e16ca2-36cc-4bb4-9ae2-8602167b6df5](https://github.com/user-attachments/assets/a7e518f5-df55-41d0-8a0f-6bede4bce5ef)</br>
```
np.sqrt(df["Highly Positive Skew"])</br>
![372038342-2b3b9469-a49c-4285-8c53-6158025da034](https://github.com/user-attachments/assets/ec6801e1-21bb-446b-81ac-7977ebae9add)</br>
```
np.square(df["Highly Positive Skew"])</br>
![372038515-b2ee6d10-0ca8-4c43-8a5c-d1e425318246](https://github.com/user-attachments/assets/db6fe231-8d5a-4567-be2c-84adf0babe1a)</br>
```
df["Highly Positive Skew_boxcox"], parameters=stats.boxcox(df["Highly Positive Skew"])</br>
df</br>
![372038750-8715ef25-6571-4a90-b9a1-5d6ad36ccaf1](https://github.com/user-attachments/assets/4b9ee0f8-4e98-4c90-828e-22641b924b1a)</br>
```
df["Moderate Negative Skew_yeojohnson"],parameters =stats.yeojohnson(df["Moderate Negative Skew"])</br>
df</br>
![372039112-fda58aed-306d-4447-b66a-db7cdd0b233a](https://github.com/user-attachments/assets/87a9623b-d874-4105-9f34-524f21d0bf8f)</br>
```
sm.qqplot(df['Moderate Negative Skew'],line='45')</br>
plt.show()</br>
![372039290-e4826368-b926-4d18-bc8f-7ff61372cc92](https://github.com/user-attachments/assets/1f648e2d-ef4a-49a3-8353-920aa6084450)</br>
```
from sklearn.preprocessing import QuantileTransformer</br>
qt=QuantileTransformer(output_distribution='normal',n_quantiles=891)</br>

df["Moderate Negative Skew"]=qt.fit_transform(df[["Moderate Negative Skew"]])</br>

sm.qqplot(df["Moderate Negative Skew"],line='45')</br>
plt.show()</br>
![372039497-189e9be3-76c4-41ca-a7cf-63764cebec7b](https://github.com/user-attachments/assets/d21bf597-9d3f-4a7c-95ae-600c8edd13a7)</br>
```
df</br>
![372039731-9a74678c-3e7c-4d20-96cf-c95e1b37707a](https://github.com/user-attachments/assets/44b2e10f-9160-4d27-bba7-43b539d76acd)</br>
```
df["Moderate Negative Skew_1"]=qt.fit_transform(df[["Moderate Negative Skew"]])</br>
sm.qqplot(df['Moderate Negative Skew'],line='45')</br>
plt.show()</br>
![372039963-cdccbea2-1a33-4f3b-9ba3-95a12ac42751](https://github.com/user-attachments/assets/9688e37e-af5f-4bb8-98a6-410bd5898726)</br>
```
df["Highly Negative Skew_1"]=qt.fit_transform(df[["Highly Negative Skew"]])</br>
sm.qqplot(df['Highly Negative Skew'],line='45')</br>
plt.show()</br>
![372040112-c2a44890-9aee-4a59-808c-e5e43bd57817](https://github.com/user-attachments/assets/eb2ecdd2-0b96-4017-b36a-6990807b0c61)</br>
```
sm.qqplot(df["Highly Negative Skew_1"],line='45')</br>
plt.show()</br>
![372040288-b42704ee-86d4-4dee-8d41-544235bf59e3](https://github.com/user-attachments/assets/15d8612a-71ba-4fab-b995-6ecad5d57e68)</br>
```
sm.qqplot(np.reciprocal(df["Moderate Negative Skew"]),line='45')
plt.show()</br>

![image](https://github.com/user-attachments/assets/c6dcd68b-046d-484a-9777-65e2d5797609)


```
# RESULT:
  
  Thus the given data, Feature Encoding, Transformation process and save the data to a file was performed successfully.
       
