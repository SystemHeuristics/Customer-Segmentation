# Rule Mining on  heartdisease dataset using WEKA.

Information of attributes: This data is about heart data, given that there are some attributes like age, gender, restecg, cholesterol, resting blood pressure and some more attributes, where class predict that the person have heart disease or not.
Gender: Attribute is categorical and binary. There are only two possible values for this attribute that is gender is male or gender is female.
Age: This attribute has continuous vales. Age shows the age of the person to see if he/she have heart disease or not. We will discretize this attribute before applying association rule mining on data.
CP: This represents Chest Pain type. There are 4 types of chest pain.
•	Value 1: typical angina
•	Value 2: atypical angina
•	Value 3: non-anginal pain
•	Value 4: asymptomatic     
Trestbps: This attribute is also continuous and we will discretize it before applying rules. This gives information about resting blood pressure sugar.
Chol: This attribute shoes quantity of the serum in mg or dl. This is also a continuous attribute and we will discretize it before using in association rule.
Fbs: This is a fasting blood sugar value which come in continuous type. But this has been classified to make it a categorical value. Such that the value above 120 mg/dl are classified as true and the values below 120 mg/dl are classified as false.
Thalach: it is also a continuous attribute that shows the maximum heart rate achieved for a person. We will discretize the attribute before associate rule mining.
Exang: shows the person is doing exercise to prevent angina or not. The answer is binary: yes or no.
oldpeak: Depression that maybe induced due to rest related exercise.
slope: This is an oldpeak dependent categorical attribute with three values:
•	Value 1: upsloping
•	Value 2: flat
•	Value 3: downsloping
ca: Categorical variable that shows number of major vessels. From 0-3 as colored by fluoroscopy.
thal: Categorical variable that shows values as 3 = normal; 6 = fixed defect; 7 = reversable defect.
class: Class nu,ber shpws diagnosis of heart disease in which values less than 50% are classified as 0 and values greater than 50% are marked as 1.


Question 1 part A
PCA
We will preprocess the data to apply PCA
Preprocessing:
Missing Values:
Remove attributes that have 50% or greater than 50% missing values. In Weka there is option of remove below the attributes. We will select slope, ca, and thal which have 50%, 98% and 78% missing values respectively.
Now we are left with 11 attributes. For the attributes that have less than 50% missing values will be filled. We will fill them by their mean with a filter in weka.filters.unsupervised.attributes.replacemissingvalues.
Repetition:
We will delete the repeated values by using weka.filters.unsupervised.Instance.removeDuplicates.
Normalization: PCA is affected by the scale of values. So we should better normalize the data before applying the PCA. But when we apply correlation the data is automatically normalized, so in our case we will not normalize the data and use correlation.
PCA:
Applying PCA:
•	Now we are ready to apply PCA on data. We will go to select attributes option in weka and choose PrincipleComponents in attribute evaluator and change the variance to 90% as we want to cover 90% variance by the selection of the features.
•	Using PCA we want to reduce features and extract only those features that have maximum information.
•	We can choose how much variance we want to cover in selected features from weka.Select Attributes.PrincipleComponent and Variance as a parameter.
1.	For 90% variance
•	For data reduction we will use PCA which will reduce the dimensionality of data. We will use 90% variance to select the features that means we will select only those features which covers 90% variance.
•	So as first step of PCA we calculate correlation matrix
 
Figure 1: correlation of attributes

•	After getting correlation matrix we will calculate Eigen values and eigenvectors.
 

 
Figure 2: Eigen Vectors
•	After having eigenvalues and eigenvectors we will arrange them and get the desired features.
•	For covering 90% variance we got 9 features.
•	We can choose the features with two methods, either choose those features that covers 90% variance. So final results are:
 
Figure 3: Attributes after reduction

2.	By Choosing 95% variance
•	Correlation of features is same no matter how much variance we choose.
•	These are the selected Eigen values that cover 95% variance.
 
 
Figure 4: Eigen vectors
•	After having eigenvalues and eigenvectors we will arrange them and get the desired features.
•	While covering 95% variance we got 10 features.
•	We can choose the features with two methods, either choose those features that covers 95% variance. So final results are:
 
Figure 5: PC’s from Eigen Vectors

3.	By having 85% variance
•	Lets say we want to get the features that cover 85% of the variance.
•	Correlation is the first step in PCA. And this is same for all the variance coverage.
•	Now calculate eigen vectors and eigen values.
 
Figure 6: PC’s from Eigen Vectors

•	Ranked attributes according to the variance coverage of 85% are: 
 
Figure 7: Ranked attributes from eigen vectors
•	The other method is we can choose the resulting dimension of our features that means we can select how many features we want at the end. 













1.	Lets see I want 5 features at the end, so this will be result of my PCA.
 
Figure 8: PC’s after selecting 5 features.
2.	Now lets choose 9 attributes and see the results:
•	Correlation is same for all the vectors.
•	These are eigen vectors and the ranked list of attributes.
 
Figure 9: PC’s after selecting 9 features.

b- Name the attributes that you have selected and state the reason.
•	Now we are considering the attributes that cover 90% of the variance. From those we will select the features that have principle component value greater than 0.5.
•	As we have defined the importance criteria as |0.5| so  we can find important attributes from PC’s given in the picture below.
 
Figure 10: Important features from PC

•	From PC1 We don’t have any value that have greater than 0.5 value, so no attribute will be selected from that feature.
•	From PC2 -.5432 value corresponding to fbs, so fasting blood sugar will be selected as it have high importance.
•	From PC3 we have -0.569 value of chol that means chol is important and we should select it.
•	From PC4 we have -0.522 thalach, value shows the importance of thalach, so we will select it.
•	From PC5 -0.692 gender and the value shows the importance of gender, so we will select it.
•	From PC6 we don’t have any attribute value greater than |0.5|
•	From PC7 -0.612 restecg and the value shows the importance of restecg, so we will select it.
•	From PC8 0.617 cp and the value shows the importance of cp, so we will select it.
•	From PC9 0.655exang and the value shows the importance of exang, so we will select it.
So the selected features are:
Fbs: The data is from the domain of heart disease and fbs represents fasting blood sugar. If fasting blood sugar is greater than 120 then there is a fear of attack or something more dangerous, so it must be taken care of to prevent any disease.
Chol: Chol is the quantity of the serum in mg/dl. That shows either the person is taking medicine for disease prevention or not. As cholesterol is directly related to heart and if a person has high cholesterol then there are higher chances of heart disease in that person.
Thalach: thalach shows the maximum heartbeat rate. As we know 60-100 beats per minute is a normal rate of heart beat for a person. So if the thalach is high it means there is definitely some problem that can effect heart.
Gender: Heart diseases are also related to gender. Such as men are prompt to have heart disease as compared to women.
Restecg: This attribute shows values of a person in normal posture (not running, exercising etc.) so the normal ecg rate can be seen. Then the ECG values while resting are categorized. So if a person doesn’t have normale values then he must have a checkup as abnormality in values shows abnormality in body that directly effect the heart.
Cp: This attribute indicates chest pain. Heart attack’s initial symptom includes left arm pain and chest pain, so if a person is feeling chest pain then he/she must have a problem within heart.
Exang: Attrribute shows warn up angina this type of angina directly affects the heart and may cause a problem. So it is important to select this attribute to see its effects on heart.
Question Number 2:
Association rule minning
a)	Use confidence as an interestingness measure of an association rule. Rank the top 10 association rules for at least the three different combinations of support and confidence. Explain the rules and why you consider them interesting and valuable. Furthermore, also give recommendations based on the discovered rules that might help the user.
Answer:
For association rule mining we have to preprocess data before mining the rules.
Preprocessing:
Missing Values:
Remove attributes that have 50% or greater than 50% missing values. In Weka there is option of remove below the attributes. We will select slope, ca, and thal which have 50%, 98% and 78% missing values respectively.
Repetition:
We will delete the repeated values by using weka.filters.unsupervised.Instance.removeDuplicates.
Data Type:
As association is applied on categorical data and our dataset is in numeric form, so first we will change the data to categorical data.
So to change the data to categorical data we will open the file in notepad and change the attributes type to categorical.
@attribute gender {0,1}
@attribute cp {1,2,3,4}
@attribute chol numeric
@attribute fbs {0,1}
@attribute restecg {0,1,2}
@attribute thalach numeric
@attribute exang {0,1}
@attribute class {0,1,2,3,4}
Discretization:

•	If we take small intervals for discretization then support will not be enough.
•	If we select large intervals the confidence will not be enough.
•	Continuous attributes will be discretized to be represented as categorical. Because association can be applied only on categorical data. So we have chol and thalach as continuous variables and we will discretize them to make them categorical data.
•	Weka.filters.unsupervised.discretize and from options we will make bins=number of classes=5 from the options of discretization and we will mark useEqualFrequency as True to make equal number of elements in each bin.
 
Figure 11: Discretization settings

Thalach:
 
Figure 12: Bins for thalach






Chol:
 
Figure 13: Discretization of chol
Now all the data is nominal and we are ready to apply Association on it to make rules.
Weka.association.apriori
Support and confidence: The measure shows how often a an appeared attribute in the list appeared trule.
We will study 5 different conditions for different values of support and confidence.
1.	Minimum support=0.4 and minimum confidence =1.0
 
Figure 14: Example of no rules with Minimum support=0.4 and minimum confidence =1.0
•	No rules found.
•	We are trying to make rules that have 100% confidence. But in this dataset there exists no such rule that have 100% confidence. 12 iterations are performed but no rule is found in this condition.







2.	Minimum support=0.1 and minimum confidence=0.45
 
Figure 15: Example of rules with Minimum support=0.1 and minimum confidence =0.45
Rule 1: If chest pain (cp) is of type then the person is more likely to be male. This rule is important because it has 91% confidence that if there are 352 asymptomatic chest pain type then 322 of those person are male. This rule is also important because there is confidence of 91% for relationship of cp=4 and male.
Recommendation: Rule says that an asymptomatic chest pain is most likely to occur in male. Asymptomatic chest pain is a severe representation of heart attack, so if a person is feeling it he must visit doctor so the risk of heart attack may lessen.
Rule 2: A person with normal ECG while resting says that he is a male. This rule is important with 83% confidence. Importance of the rule can also be seen by the relationship between the attributes that shows out 399 normal resting ECG 330 are male.
Recommendation: mostly male people have normal ECG while resting.
Rule 3: if a person is taking fbs in less than 120mg quantity then he is a male. The rule is strong and interesting with 82% confidence. Interestingness of the rule can also be seen by the relationship between the 2 attributes which says if there are 432 fbs smaller than 120mg 354 of them are male. That shows the change one attribute will definitely affect the other.
Recommendation: Male person should have dose of fbs less than 120mg/dl.
Rule 4: If a person’s exercise is not inducing angina then then he is most likely to be male. This rule is important with 77% confidence.
Recommendation: Man should exercise regularly to be active, if he is not healthy don’t feel lazy or don’t be afraid that exercise can harm you, be active this can save you from many other diseases.
Rule 5: A person with normal ECG while resting says that he is having fbs less than 120mg/dl. This rule is important with 75% confidence. Importance of the rule can also be seen by the relationship between the attributes that shows out 399 normal resting ECG 299 of them are taking fbs<120mg.
Recommendation: If a person wants to be healthy and wants his ecg to be normal while resting he must lessen his fbs dose below 120dl.
Rule 6: if a person is taking fbs less than 120mg then his ecg is most likely to be normal. This rule is important with confidence of 69%.
Recommendation: Increasing or decreasing the fbs dose doesn’t affect the ECG while resting.
Rule 7: Male people are consuming fbs less then 120mg are. This rule has confidence of 68%.
Recommendation: if the user is female then she should take the fbs dosage carefully as it can affect the restecg results.
Rule 8: If a person is male then his rest ECG is morelikely to be normal. This rule is important with confidence of 64%.
Recommendation: Male people are more healthy as compare to female people. Female should take care of their lives so they can spend healthy life.
Rule 9 : Male gender are more likely to have of asymptomatic chest pain. This rule is important with 62% confidence.
Recommendation: Male can also have other chest pain as pain is independent of gender, so users should take care of their routine.
Rule 10: if the person is male then it is more likely to happen that his exercise doesn’t induce angina. This rule is important with 48% confidence.
Recommendation: a male person should exercise daily to be active, there is no side effect of exercise nor his exercise will induce angina.
3.	Minimum support= 0.3, minimum confidence=0.7
 
Rule 1: If exercise induced angina then there is high probability that the person is male. This is seen in 216 male with confidence of 91%. This rule is important because it has 91% confidence. Importance of the rule can also be seen that out of 237 people having exercise induced angina 216 of them are male. Although exercise should affect both gender equally but surprisingly this rule shows its effect in man that shows its importance.
Recommendation: Exang is exercised that induces angina, so if the person is feeling angina he should start the exercise gradually and should not stop the exercise suddenly because activity can help in curing the angina so you should keep yourself active rather being lazy by stopping the exercise.
Rule 2: If chest pain (cp) is of type asymptomatic and fasting blood sugar (fbs) is less than 120 mg/dl then the person is more likely to be male. This rule is important because it has 91% confidence that if there is a relation between asymptomatic chest pain type with fbs less than 120mg then the person is male. This rule is also important because there is relationship of cp (asymptomatic) and fbs (120mg/dl) 226 times and 205 times the gender was found to be male.
Recommendation: Rule says that a asymptomatic chest pain and fbs less than 120mg is found in male. Asymptomatic chest pain is a severe representation of heart attack, so if a person is feeling it he must increase the dose of fbs greater than 120mg so the risk of heart attack may lessen.
Rule 3: If a person is feeling asymptomatic chest pain and their restecg is normal then a person is more likely to be male. The rule is important because it has 90% confidence as 221 relationships are seen in asymptomatic chest pain and 200 of them are found to be men.
Recommendation: If a man is feeling asymptomatic chest pain and his ECG is normal he should not take it easy, asymptomatic pain can lead to heart attack, he should immediately have some medicine.
Rule 4: Class shows if the artery diameter narrowing is less than 50% or not. So if the artery diameter narrowing is greater than 50% then the person is more likely to be man with confidence of 90%. This is a strong rule with 90% confidence that shows its interestingness that shows that men has narrow diameter greater than 50%.
Recommendation: If class has artery diameter of greater than 50% then the person is more likely to be a man with confidence of 90%. As arteries provide oxygen to users, so getting it wide or narrowing down may affect the quantity of oxygen supplied to heart, so if an artery is wide than there is excessive oxygen supply to heart and the man should immediately visit his doctor.
Rule 5: if a person has artery narrowed down and diameter is less than 50% then it is most likely that fbs is less than 120mg. this rule is important as it has 86% confidence and out of 246 narrow diameter arteries 211 of them has less than 120mg fbs.
Recommendation: he/she should increase quantity of fbs serum so his arteries remain normal and do not narrow down. As narrowing down the arteries may cause difficulty in breathing.
Rule 6: if a person has exercise induced angina then the person is most likely to have asymptomatic chest pain. This rule is important with 83% confidence. Its interestingness is also shown by the rule implication which shows that if there are 237 exercise induced angina then 196 of them have asymptomatic chest pain.
Recommendation: the person having exercise induces angina is most likely to have asymptomatic chest pain so he should better avoid the exercise or continue the exercise in careful manner.
Rule 7: if a person is taking fbs in less than 120mg quantity and his restecg is normal the he is a male. The rule is strong and interesting with 81% confidence. Interestingness of the rule can also be seen by the relationship between the 2 attributes in which there is a relationship between 299 fbs smaller than 120mg and normal restecg and 241 of them are male. That shows the change one attribute will definitely affect the other.
Recommendation: User should have fbs less than 120mg/dl so his ECG can be normal. This will mostly help a male person.
Rule 8: if a person has diameter narrow below 50% then his restECG is probably normal. This rule is interesting with confidence of 79%. This is surprising than a narrow artery has normal ECG while resting, that make it an important rule.
Recommendation: the person should take care of his diet and make his arteries narrowed below 50% diagram so his ECG can be normal.
Rule 9: If a person’s exercise is not inducing angina then then he is most likely to be male. This rule is important with 77% confidence.
Recommendation: Man should exercise regularly to be active, if he is not healthy don’t feel lazy or don’t be afraid that exercise can harm you, be active this can save you from many other diseases.
Rule 10: a person with normal ECG while resting says that he is having fbs less than 120mg/dl. This rule is important with 75% confidence. Importance of the rule can also be seen by the relationship between the attributes that shows out 399 normal resting ECG 299 of them are taking fbs<120mg.
Recommendation: If a person wants to be healthy and wants his ecg to be normal while resting he must lessen his fbs dose below 120dl.

4.	Minimum support= 0.35, minimum confidence=0.8

 
Figure 16: Example of rules with Minimum support=0.35 and minimum confidence =0.8
Rule 1: If exercise induced angina then there is high probability that the person is male. This is seen in 216 male with confidence of 91%. This rule is important because it has 91% confidence. Importance of the rule can also be seen that out of 237 people having exercise induced angina 216 of them are male. Although exercise should affect both gender equally but surprisingly this rule shows its effect in man that shows its importance.
Recommendation: Exang is exercised that induces angina, so if the person is feeling angina he should start the exercise gradually and should not stop the exercise suddenly because activity can help in curing the angina so you should keep yourself active rather being lazy by stopping the exercise.
Rule 2: if a person is taking fbs in less than 120mg quantity and his restecg is normal the he is a male. The rule is strong and interesting with 81% confidence. Interestingness of the rule can also be seen by the relationship between the 2 attributes in which there is a relationship between 299 fbs smaller than 120mg and normal restecg and 241 of them are male. That shows the change one attribute will definitely affect the other.
Recommendation: User should have fbs less than 120mg/dl so his ECG can be normal. This will mostly help a male person.
5.	Minimum support= 0.35, minimum confidence=0.6

 
Figure 17: Example of rules with Minimum support=0.34 and minimum confidence =0.6
Rule 1: If chest pain (cp) is of type then the person is more likely to be male. This rule is important because it has 91% confidence that if there are 352 asymptomatic chest pain type then 322 of those person are male. This rule is also important because there is confidence of 91% for relationship of cp=4 and male.
Recommendation: Rule says that an asymptomatic chest pain is most likely to occur in male. Asymptomatic chest pain is a severe representation of heart attack, so if a person is feeling it he must visit doctor so the risk of heart attack may lessen.
Rule 2: If exercise induced angina then there is high probability that the person is male. This is seen in 216 male with confidence of 91%. This rule is important because it has 91% confidence. Importance of the rule can also be seen that out of 237 people having exercise induced angina 216 of them are male. Although exercise should affect both gender equally but surprisingly this rule shows its effect in man that shows its importance.
Recommendation: Exang is exercised that induces angina, so if the person is feeling angina he should start the exercise gradually and should not stop the exercise suddenly because activity can help in curing the angina so you should keep yourself active rather being lazy by stopping the exercise.
Rule 3: A person with normal ECG while resting says that he is a male. This rule is important with 83% confidence. Importance of the rule can also be seen by the relationship between the attributes that shows out 399 normal resting ECG 330 are male.
Recommendation: mostly male people have normal ECG while resting.
Rule 4: if a person is taking fbs in less than 120mg quantity then he is a male. The rule is strong and interesting with 82% confidence. Interestingness of the rule can also be seen by the relationship between the 2 attributes which says if there are 432 fbs smaller than 120mg 354 of them are male. That shows the change one attribute will definitely affect the other.
Recommendation: Male person should have dose of fbs less than 120mg/dl.
Rule 5: if a person is taking fbs in less than 120mg quantity and his restecg is normal the he is a male. The rule is strong and interesting with 81% confidence. Interestingness of the rule can also be seen by the relationship between the 2 attributes in which there is a relationship between 299 fbs smaller than 120mg and normal restecg and 241 of them are male. That shows the change one attribute will definitely affect the other.
Recommendation: User should have fbs less than 120mg/dl so his ECG can be normal. This will mostly help a male person.
Rule 6: If exercise does not induce angina then there is high probability that the person is male. This is seen in 250 male with confidence of 77%. This rule is important because it has 77% confidence. Importance of the rule can also be seen that out of 322 people having exercise induced angina 250 of them are male. Although exercise should affect both gender equally but surprisingly this rule shows its effect in man that shows its importance.
Recommendation: Exang is exercise that induces angina, so if the person is feeling angina he should start the exercise gradually and should not stop the exercise suddenly because activity can help in curing the angina so you should keep yourself active rather being lazy by stopping the exercise.
Rule 7: A person with normal ECG while resting says that he is having fbs less than 120mg/dl. This rule is important with 75% confidence. Importance of the rule can also be seen by the relationship between the attributes that shows out 399 normal resting ECG 299 of them are taking fbs<120mg.
Recommendation: If a person wants to be healthy and wants his ecg to be normal while resting he must lessen his fbs dose below 120dl.
Rule 8:
If a male person has rest ECG normal then he is taking fbs dose less than 120mg. This rule is important with 73% confidence.
Recommendation:
If a male person is taking dose of fbs greater than 120mg he should decrease the dose as this will most likely to have heart disease if the dose is increased.
Rule 9:
If a person does not induce angina during exercise then his resting ECG is normal. This rule is important with 71% confidence.
Recommendation: A person should have careful exercise so it does not induce angina and his ECG shows normal results.
Rule 10:
If a person does not induce angina during exercise then he is taking dose of fbs less than 120mg. This rule is important with 70% confidence.
Recommendation: A person should take less quantity of fbs if he doesn’t want his  exercise to induce angina.

Question 2 part b
Use interest as an interestingness measure of an association rule. Rank the top 10 association rules for at least three combinations of support and interest. Explain the rules and why you consider it interesting and useful. Furthermore, also give recommendations based on the discovered rules that might help the user.
Answer: 
1.	Min support=20% and attributes are positively related with lift=1.5.
 
Figure 19: Example of no rules with Minimum support=0.2 and minimum confidence =1.5
Rule 1:
If a person is taking fbs dose less then 120mg and his exercise is not inducing angina then he is most likely to have normal ECG while resting and diameter narrow to 50%. This rule is important with 56% confidence and lift of 2.02. That shows that the attributes are positively associated to each other.
Recommendation: A person should have low dose of fbs in order to have normal ecg and narrow arteries.
Rule 2:
If a person have normal ECG while resting and diameter narrow to 50% then he is taking fbs dose less then 120mg and his exercise is not inducing angina. This rule is important with 74% confidence and lift of 2.02. That shows that the attributes are positively associated to each other.
Recommendation: A person having normal ecg while resting and narrow entries should have fbs dose less than 120mg.
Rule 3: A person having narrow diameter below 50% is taking fbs less than 120mg and his exercise is not inducing angina. This rule is important with 69% confidence and the attributes are positively associated with lift of 1.86.
Recommendation: Lessing down the quantity of fbs and when the exercise is not inducing angina artries diameter will narrow down to 50% so he should take a proper quantity of the fbs and a proper and careful exercise.
Rule 4: if a person is taking fbs is less than 120mg and the exercise is not inducing angina then his artries most likely to narrow down 50%. This is an important rule with confidence of 74% and lift= 1.86 that shows that the attributes are positively associated.
Rule 5:
If a person is having narrow diameter of arteries below 50% then he is taking less than 120 mg fbs and his resting ECG is normal and his exercise is not inducing angina. This rule is interesting with 52% confidence and lift=1.86 that shows that the attributes are positively related.
Recommendation: People with narrow arteries should take fbs dose less then 120 mg. and there exercise should not induce angina.
Rule 6: If a person has fbs less than 120 mg, his resting ecg is normal and his exercise is not inducing angina then his arteries are narrowing down. This rule is important with 74% confidence and 1.86 lift for positive association of attributes.
Recommendation: A person should have less than 120mg fbs to have all the reports normal.
Rule 7: If a person have fbs less than 120mg and his arteries diameter below 50% then he has resting ECG normal and his exercise is not inducing angina. This rule is important with 61% confidence and 1.84 lift for positive association of attributes.
Recommendation: A person should have less than 120mg fbs to have all the reports normal.
Rule 8: if a person has resting ecg normal and his exercise is not inducing angina then theperson has fbs less than 120 mg and his arteries are narrowing down. Rule is interesting with confidence of 56% and lift=1.84.
Recommendation: A person should have less than 120mg fbs to have all the reports normal.
Rule 9: If a person’s exercise is inducing angina then he is a male and he has asymptomatic chest pain and he is taking fbs less than 120mg. This rule is important with 54% confidence and 1.41 lift.
Recommendation: User should have dose of fbs less then 120 mg if he wants all his reports normal.
Rule 10: If a person is male then he is feeling asymptotic chest pain and he is taking fbs dose less then 120mg then his exercise is inducing angina. This rule is interesting with 62% confidence and lift of 1.61.
Recommendation: person should increase fbs does in order to be safe from angina.
2.	Minimum support 0.35, lift=1

 
Figure 20: Rules with Minimum support=0.35 and minimum Lift =1.0
Rule 1: Normal restecg is independent of exercise that induces angina. This attribute is important with confidence of 57% and lift=1.05.
Recommendation: Having exercise doesn’t affect ECg while resting so the user can have exercise independent of ECG.
Rule 2: Angina induction from exercise is independent of ECG while resting. This rule is important with confidence of 71% and lift of 1.09.
Recommendation: If a person is feeling angina pain then maybe its not shown in the ECG report, so he should be careful about this.
Rule 3: Male gender is independent of asymptomatic chest pain. This rule is important with 62% confidence.
Recommendation: Male can also have other chest pain as pain is independent of gender, so users should take care of their routine.
Rule 4: Chest pain of type asymptomatic is independent of male. This rule is interesting with 91% confidence with lift of 1.09.
Recommendation: Chest pain is independent of Gender so person should be very careful about their routine.
Rule 5: Male are independent of exercise inducing angina. This rule is important as it have confidence of 42%.
Recommendation: Angina pain can occur in male and female both, so be careful about this.
Rule 6: Exercise inducing angina is independent of male people. This rule is important as it have confidence of 91%.
Recommendation: Angina pain can occur in male and female both, so be careful about this.
Rule 7: RestEcg is independent of quantity of fbs. This rule is important as it have confidence of 69%.
Recommendation: increasing or decreasing the fbs dose doesn’t effect the ECG while resting.
Rule 8: Restingecg is independent og fbs quantity. This rule is important with 75% confidence.
Recommendation: changong the quantity of fbs doesn’t effect the reports of resting ecg are normal.
Rule 9: Restecg is independent of gender if the quantity of fbs is less then 120mg. this rule is important with 60% confidence.
Recommendation: IF the male person is taking fbs less then 120mg then the resting ECG results are independent of the dosage of fbs.
Rule 10: Male people having fbs less then 120mg are independent of the results of normal resting ecg. This rule has confidence of 68%.
Recommendation: if the user is female then she should take the fbs dosage carefully as it can affect the restecg results.
3.	Min support=0.5, Min lift=-0.7

 
Figure 21: Rules with Minimum support=0.5 and minimum lift=0.7
There are 6 rules that are negatively associated when their support is 0.5.
Rule 1: Male gender are more likely to have of asymptomatic chest pain. This rule is important with 62% confidence.
Recommendation: Male can also have other chest pain as pain is independent of gender, so users should take care of their routine.
Rule 2: Chest pain of type asymptomatic is more likely to occue in male. This rule is interesting with 91% confidence with lift of 1.09.
Recommendation: Chest pain is independent of Gender so person should be very careful about their routine.
Rule 3: Restecg is independent of gender if the quantity of fbs is less then 120mg. this rule is important with 60% confidence.
Recommendation: IF the male person is taking fbs less then 120mg then the resting ECG results are independent of the dosage of fbs.
Rule 4: Male people having fbs less then 120mg are independent of the results of normal resting ecg. This rule has confidence of 68%.
Recommendation: if the user is female then she should take the fbs dosage carefully as it can affect the restecg results.
Rule 5: Male people are consuming fbs less then 120mg are. This rule has confidence of 68%.
Recommendation: if the user is female then she should take the fbs dosage carefully as it can affect the restecg results.
Rule 6: Most of the people having dose of fbs less then 120mg are male. This rule has confidence of 82%. The attributes are negatively associated.
Recommendation: Male people may have negative affect of fbs if they consume it in more than 120mg quantity.
Question 2 Part c
Try to formulate some questions that you want to ask of your rule learning extraction systems. Select the attributes that will be required to answer your questions. Run Association rule mining to extract interesting patterns. Show at least 10 rules. Explain the rules and why you consider them interesting and useful. Explain what insight you got regarding your questions.

1.	My question: Age is also a major factor why it has no association with other attributes?
As answer to my question I will consider age as 9th feature and make rules with this feature as well. 
Insights of my question. Gender is directly positively related cholesterol level with 94% confidence, so this is a rule of high importance. But it seems to not have any relation with other attributes.
	We minimum support 0.4 and minimum confidence 0.45
 
Figure 22: Rule with min support 0.4 and confidence 0.45
Rule 1: If chest pain (cp) is of type then the person is more likely to be male. This rule is important because it has 91% confidence that if there are 352 asymptomatic chest pain type then 322 of those person are male. This rule is also important because there is confidence of 91% for relationship of cp=4 and male.
Recommendation: Rule says that an asymptomatic chest pain is most likely to occur in male. Asymptomatic chest pain is a severe representation of heart attack, so if a person is feeling it he must visit doctor so the risk of heart attack may lessen.
Rule 2: A person with normal ECG while resting says that he is a male. This rule is important with 83% confidence. Importance of the rule can also be seen by the relationship between the attributes that shows out 399 normal resting ECG 330 are male.
Recommendation: mostly male people have normal ECG while resting.
Rule 3: if a person is taking fbs in less than 120mg quantity then he is a male. The rule is strong and interesting with 82% confidence. Interestingness of the rule can also be seen by the relationship between the 2 attributes which says if there are 432 fbs smaller than 120mg 354 of them are male. That shows the change one attribute will definitely affect the other.
Recommendation: Male person should have dose of fbs less than 120mg/dl.
Rule 4: If a person’s exercise is not inducing angina then then he is most likely to be male. This rule is important with 77% confidence.
Recommendation: Man should exercise regularly to be active, if he is not healthy don’t feel lazy or don’t be afraid that exercise can harm you, be active this can save you from many other diseases.
Rule 5: A person with normal ECG while resting says that he is having fbs less than 120mg/dl. This rule is important with 75% confidence. Importance of the rule can also be seen by the relationship between the attributes that shows out 399 normal resting ECG 299 of them are taking fbs<120mg.
Recommendation: If a person wants to be healthy and wants his ecg to be normal while resting he must lessen his fbs dose below 120dl.
Rule 6: if a person is taking fbs less than 120mg then his ecg is most likely to be normal. This rule is important with confidence of 69%.
Recommendation: Increasing or decreasing the fbs dose doesn’t affect the ECG while resting.
Rule 7: Male people are consuming fbs less then 120mg are. This rule has confidence of 68%.
Recommendation: if the user is female then she should take the fbs dosage carefully as it can affect the restecg results.
Rule 8: If a person is male then his rest ECG is morelikely to be normal. This rule is important with confidence of 64%.
Recommendation: Male people are more healthy as compare to female people. Female should take care of their lives so they can spend healthy life.
Rule 9 : Male gender are more likely to have of asymptomatic chest pain. This rule is important with 62% confidence.
Recommendation: Male can also have other chest pain as pain is independent of gender, so users should take care of their routine.
Rule 10: if the person is male then it is more likely to happen that his exercise doesn’t induce angina. This rule is important with 48% confidence.
Recommendation: a male person should exercise daily to be active, there is no side effect of exercise nor his exercise will induce angina.
	Minimum support=0.2, minimum confidence=0.9
 
Figure 23: Rule with min support 0.2  and confidence 0.9
Rule 1: If cholesterol is less then 42.5 then the gender is male. The attributes are positively correlated. This rule is important with 94% confidence.
Rule 2: if age is between 55-60 then the person is more likely to be male. This rule has confidence of 94%. But this is not a good assumption as there is no biasness in age of male and female, both can be of any age, but for this dataset may be most of the male people are of age 55-60.
Rule 3:  If chest pain is of asymptomatic type and the person’s exercise is inducing angina then the person is male. This rule has confidence of 91%. 126 out of 196 people are male from the above relationship.
Rule 4: If a person is feeling chest pain of asymptomatic type then the person is more likely to be male. This rule is important as it has confidence of 91% and it is positively related.
Rule 5: If a person is feeling chest pain of asymptomatic type and he is taking fbs less than 120mg and his exercise is inducing angina then the person is male. This rule is important with 91% confidence.
Rule 6: If chest pain is of asymptomatic type and the person’s arteries are narrowing the diameter below 50% then the person is male. This rule is important with confidence of 91%.
Rule 7: If a person’s exercise is inducing angina then he is male. This rule is strong and important with confidence of 91%.
Rule 8: if a person is feeling chest pain of asymptomatic and he is taking fbs less than 120mg then the person is male. This rule is important with 91% confidence.
Rule 9: If a person is feeling chest pain of asymptomatic type and his resting ECG is normale then he is male. This rule is important with 91% confidence.
Rule 10: If a person is taking fbs less than 120mg and his exercise is inducing angina then he is a male. This rule has confidence of 90% that shows its importance.
2.	My question: Does fbs affect arteries diameter?
Insights:
From the rules below which we studies with two different values of support and confidence. It seems like fbs is not related to diameter of arteries.
 
Figure 22: Rule with min support 0.37 and confidence 0.5
Rule 1: If a person is feeling chest pain of asymptomatic type then the person is more likely to be male. This rule is important as it has confidence of 91% and it is positively related.
Rule 2: A person with normal ECG while resting says that he is a male. This rule is important with 83% confidence. Importance of the rule can also be seen by the relationship between the attributes that shows out 399 normal resting ECG 330 are male.
Recommendation: mostly male people have normal ECG while resting.
Rule 3: If a person is taking fbs in less than 120mg quantity then he is a male. The rule is strong and interesting with 82% confidence. Interestingness of the rule can also be seen by the relationship between the 2 attributes which says if there are 432 fbs smaller than 120mg 354 of them are male. That shows the change one attribute will definitely affect the other.
Recommendation: Male person should have dose of fbs less than 120mg/dl.
Rule 4: if a person is taking fbs in less than 120mg quantity and his restecg is normal the he is a male. The rule is strong and interesting with 81% confidence. Interestingness of the rule can also be seen by the relationship between the 2 attributes in which there is a relationship between 299 fbs smaller than 120mg and normal restecg and 241 of them are male. That shows the change one attribute will definitely affect the other.
Recommendation: User should have fbs less than 120mg/dl so his ECG can be normal. This will mostly help a male person.
Rule 5: If a person’s exercise is not inducing angina then then he is most likely to be male. This rule is important with 77% confidence.
Recommendation: Man should exercise regularly to be active, if he is not healthy don’t feel lazy or don’t be afraid that exercise can harm you, be active this can save you from many other diseases.
Rule 6: A person with normal ECG while resting says that he is having fbs less than 120mg/dl. This rule is important with 75% confidence. Importance of the rule can also be seen by the relationship between the attributes that shows out 399 normal resting ECG 299 of them are taking fbs<120mg.
Recommendation: If a person wants to be healthy and wants his ecg to be normal while resting he must lessen his fbs dose below 120dl.
Rule 7:
If a male person has rest ECG normal then he is taking fbs dose less than 120mg. This rule is important with 73% confidence.
Recommendation:
If a male person is taking dose of fbs greater than 120mg he should decrease the dose as this will most likely to have heart disease if the dose is increased.
Rule 8:
If a person does not induce angina during exercise then his resting ECG is normal. This rule is important with 71% confidence.
Recommendation: A person should have careful exercise so it does not induce angina and his ECG shows normal results.
Rule 9: if a person is taking fbs less than 120mg then his ecg is most likely to be normal. This rule is important with confidence of 69%.
Recommendation: Increasing or decreasing the fbs dose doesn’t affect the ECG while resting.
Rule 10: Male people are consuming fbs less then 120mg are. This rule has confidence of 68%.
Recommendation: if the user is female then she should take the fbs dosage carefully as it can affect the restecg results.

Question 2 part d
Try some evaluation measures other than confidence and lift. Show 10 strong rules. Explain the rules and why you consider them interesting and useful.

Answer:
1.	Leverage as an interesting measure. Leverage is used to see the difference between the joint probability of 2 attributes and the probabilty of the attributes being independent.
 
Figure 25: Rule with min support 0.37 and Leverage=0
Rule 1: Male people are likely to be independent of asymptomatic chest pain as they have leverage of 0.04 that is near to 0. 
Importance: this rule is important as it shows the independence of two attributes that shows that gender is independent of the chest pain type.
Rule 2: Asymptomatic chest pain is independent of gender male as its leverage 0.04 is close to 0.
Importance: The rules shows the independence of two attributes. Change in one attribute will not affect the change in other attribute.
Rule 3: normal resting Ecg results are independent of Fbs dosage.
Importance: the rule shows independence of two attributes with leverage value of 0.03. that shows that change in fbs dosage will not affect the ecg results.
Rule 4: fbs dosage is independent of Normal resting ECG results.
Importance: Rule shows the independence of 2 attributes with leverage value of 0.03. that says that if you get normal rest ecg results and you are that fbs less than 120mg as a dose, this doesn’t mean that the normal results are because of your fbs dosage quantity.
Rule 5: No induction of angina during exercise is independent of resting ecg results.
Importance: Independence of two attributes exang and restecg is important because it tells the user that exercise is independent of ECG, so if your exercise is inducing angina that may not be shown in the ecg results.
Rule 6: Ecg doesn’t effect the induction of angina dusring exercise as  they are independent of each other.
Importance: Independence of two attributes exang and restecg is important because it tells the user that exercise is independent of ECG, so if your exercise is inducing angina that may not be shown in the ecg results.
Rule 7: Normal ECG results are independent of male gender and fbs dosage of less than 120mg
Importance:  Normal restecg is independent of fbs dosage and the male gender. So this rule is important to show that chage in anyone attribute doesn’t affect anyother attribute.
Rule 8: Normal ECG results are independent of male gender and fbs dosage of less than 120mg.
Importance: Normal restecg is independent of fbs dosage and the male gender. So this rule is important to show that chage in anyone attribute doesn’t affect anyother attribute.
Rule 9:  Male gender with normal resting ecg results are independent of the dosage less then 120mg.
Importance:  The rule shows the importance of the relation of normal restecg and male gender, and they are independent of the fbs dosage.
Rule 10: fbs dosage less then 120mg is indepednant of male gender with normal restecg results. Leverage of 0.01 shows the independence of relation ship of male and normal restecg result with fbs.
Importance: The rules shows the delationship between normal restecg results and gender male. On the same time is also showing its relationship with the dosage of fbs. 
2.	Conviction: Conviction shows how unrelated the attributes are, if the value of conviction is 1 it means that the attributes are completely unrelated.
	Minimum support 0.3, minimum conviction=1
 
Figure 26: Rule with conviction=1 and support 0.37
Rule 1: Asymptomatic chest pain are not unrelated of gender male as its conviction is 1.77
Importance: The rules shows the independence but not unrelated of two attributes. Change in one attribute will not affect the change in other attribute.
Rule 2: Ecg doesn’t effect the induction of angina during exercise as  they are not unrelated of each other. Conviction is 1.18 that shows that the attributes are independent but not unrelated.
Importance: Independence of two attributes exang and restecg is important because it tells the user that exercise is independent of ECG, so if your exercise is inducing angina that may not be shown in the ecg results.
Rule 3: fbs dosage is not unrelated of Normal resting ECG results. Conviction is 1.18 that shows that the attributes are independent but not unrelated.
Importance: Rule shows the independence of 2 attributes with conviction value of 1.13. that says that if you get normal rest ecg results and you are that fbs less than 120mg as a dose, this doesn’t mean that the normal results are because of your fbs dosage quantity. But they are not unrelated.
Rule 4: Normal resting Ecg results are independent of Fbs dosage. Conviction is 1.13 that shows that the attributes are independent but not unrelated.
Importance: the rule shows independence of two attributes with conviction value of 1.13. that shows that change in fbs dosage will not affect the ecg results.
Rule 5: Male people are likely to be independent of asymptomatic chest pain as they have conviction of 1.12 that shows that the attributes are independent but not completely unrelated.
Importance: this rule is important as it shows the independence of two attributes that shows that gender is independent of the chest pain type.
Rule 6: No induction of angina during exercise is independent of resting ecg results. The attributes have conviction of 1.1 that shows the attributes are not completely unrelated.
Importance: Independence of two attributes exang and restecg is important because it tells the user that exercise is independent of ECG, so if your exercise is inducing angina that may not be shown in the ecg results.
Rule 7: fbs dosage less then 120mg is independent of male gender with normal restecg results. Conviction of 1.09 shows the independence but shows that they are slightly related and are not completely unrelated attributes.
Importance: The rules shows the relationship between normal restecg results and gender male. On the same time is also showing its relationship with the dosage of fbs. 
Rule 8: Normal ECG results are independent of male gender and fbs dosage of less than 120mg. Conviction of 1.09 shows the independence but shows that they are slightly related and are not completely unrelated attributes.
Importance:  Normal restecg is independent of fbs dosage and the male gender. So this rule is important to show that change in anyone attribute doesn’t affect any other attribute.
Rule 9: Normal ECG results are independent of male gender and fbs dosage of less than 120mg. Conviction of 1.06 shows the independence but shows that they are slightly related and are not completely unrelated attributes.
Importance: Normal restecg is independent of fbs dosage and the male gender. So this rule is important to show that change in anyone attribute doesn’t affect any other attribute.
Rule 10:  Male gender with normal resting ecg results are independent of the dosage less then 120mg. Conviction of 1.04 shows the independence but shows that they are slightly related and are not completely unrelated attributes.
Importance:  The rule shows the importance of the relation of normal restecg and male gender, and they are independent of the fbs dosage.
