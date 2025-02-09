# Information Retrieval Assignment 4 Report—README

## Students Information
- Names: Moshe Shahar, Yonatan Klein
- IDs: 211692165, 322961764

## Project Overview

This project focuses on fine-tuning a BERT model for sentiment classification of sentences and articles into categories: `pro_i`, `pro_p`, `anti_i`, `anti_p` and `neutral`. The dataset includes sentences extracted from various newspapers, and the goal is to analyze sentiment orientation accurately.

## Methodology

### Data Preparation
- **Data Sources:** We utilized labeled datasets from previous exercises, ensuring high-quality, balanced data for training.
- **Preprocessing:** Data cleaning involved removing noisy words identified through exploratory analysis. We adjusted the keyword sets to enhance the model's focus on relevant content.
- **Splitting:** 82% of articles were used for training, with an 85-15 split for training and validation. The remaining 18% served as the test set for evaluating full articles.

### Model Selection and Fine-Tuning
- **Model Choice:** We selected a pre-trained BERT sentiment model `distilbert-base-uncased` due to its balance between performance and efficiency. It retains 97% of BERT's performance while being 60% faster and 40% smaller, making it ideal for tasks like sentiment classification where you need strong contextual understanding but also require faster training and inference times. This efficiency makes it suitable for large datasets without compromising much on accuracy.
- **Fine-Tuning:** Conducted with up to 10 epochs, halting early if no improvements were observed over 5 consecutive epochs. Hyperparameters were optimized based on validation performance.

## Challenges Faced

- **Ambiguity in Sentiment:** Some sentences contained nuanced language, making sentiment hard to classify even for humans.
- **Context Dependence:** Sentences out of context sometimes led to misclassification, highlighting BERT's limitations in understanding broader narratives.
- **Data Imbalance:** Despite efforts, maintaining perfect class balance was challenging, slightly biasing the model toward more prevalent classes.

## Results and Analysis

### Performance Metrics
- **Precision, Recall, F1-Score, Accuracy:**

---

![Performance Metrics Image](images\\performance_metrics.png)

---

### Correct Classifications
- **Pro-Israeli Sentences:**
  1. "After receiving another pledge from netanyahu for funds this week, kashriel thanked the prime minister, along with regev and katz, for the help." (Score: 0.81)
  2. "Two highly experienced security guards that were at the checkpoint at the city entrance neutralized the terrorist immediately, with bravery and a lot of resourcefulness and without fear." (Score: 0.51)
  3. "Despite the ongoing tensions, the idf views the overall strategic-security situation as having improved compared with previous years." (Score: 0.50)

- **Pro-Palestinian Sentences:**
  1. "He offered them encouragement in the knowledge that in the final analysis they would all return home in peace and by the grace of god." (Score: 0.86)
  2. "“Today, I proudly stand with france to support freedom and democracy around the world”." (Score: 0.85) 
  3. "“The recognition of palestine is not against anyone, least of all israel, a friendly nation that spain values and holds in high regard and with whom we aim to foster the strongest possible relationship,” he said on the steps of moncloa palace, the prime minister’s residence, in madrid." (Score: 0.64)

- **Neutral Sentences:**
  1. "Defense officials said that while the military does not see another war breaking out, preparations for another round of conflict in the strip are conducted regularly (Score: 0.74)
  2. "The amount permitted to enter would be decided on a situational basis according to the morbidity situation and humanitarian situation." (Score: 0.77)
  3. "But the capabilities of the idf are not cheap, he said, and neither are the munitions and other weapons that the military needs." (Score: 0.68)

- **Anti-Israeli Sentences:**
  1. "In her video, dozens of right-wing protesters can be seen gathered around the activist, calling her a “whore for arabs” and threatening to harm her as border police forces who were at the scene protected her and escorted her from the scene back to her car." (Score: 0.40)
  2. "Rocks were thrown at israel police and border police officers on the temple mount tuesday night, the israel police spokesperson announced." (Score: 0.81)
  3. "Hanoi also called on Israel to stop settlement activity and to halt “forced evictions” of Palestinians and “home demolitions”." (Score: 0.72)

- **Anti-Palestinian Sentences:**
  1. "Sarah Alderawy, an unrwa teacher in gaza, took to facebook on october 7 to post a video of hamas terrorists shooting at israeli cars that day." (Score: 0.82)
  2. "IDF releases names of 5 reservists killed fighting hamas in gaza." (Score: 0.80)
  3. "“They are using their civilians as human shields,” he said, referencing the fact that hamas places its infrastructure in civilian areas." (Score: 0.52)

### Errors and Misclassifications
#### 20 Misclassified Sentences: Analysis revealed common issues such as ambiguous wording and sarcasm. For example:
- **Pro-Israeli Sentences:**
  - ""Yossi was a man of kindness and truth, of family and community, and of education in every fiber of his being, who taught hundreds of the city's children," jerusalem mayor moshe lion said." (Score: 0.84 - misclassified as `pro-p`)
  - "Intelligence and operational cooperation, along with joint exercises with foreign and regional countries, are also helping israel's security and are of great significance, the military believes." (Score: 0.71 - misclassified as `pro-p`)
  - "A year after the signing of the abraham accords, which led to the normalization of relations with several arab countries, the potential for cooperation and the building of significant military manpower is already evident." (Score: 0.64 - misclassified as `pro-p`)
  - "The people of israel are lucky to have you as their new prime minister." (Score: 0.77 - misclassified as `pro-p`)
  - "“This shows the capabilities of the idf that we will continue to develop,” he said." (Score: 0.87 - misclassified as `pro-p`)

- **Pro-Palestinian Sentences:** 
  - "It points out all the ways in which it has worked to get much more aid into gaza since october, including opening more crossings, allowing the us to create a pier on the shoreline of gaza." (Score: 0.48 - misclassified as `neutral`)
  - "“hamas can now see that the international community is united, united behind a deal that will save lives and help palestinian civilians in gaza start to rebuild and heal,” ms." (Score: 0.41 - misclassified as `anti_p`)

- **Neutral Sentences:**
  - "Revivi said he intends to use his ability to serve as a bridge between the us and israel in his next endeavor, adding that he does not know whether this will be in the political arena, the jewish relations arena, or elsewhere." (Score: 0.53 - misclassified as `pro-p`)
  - "Negotiations for a truce and a deal that would see the israeli hostages being held by hamas released could have a calming effect on the region." (Score: 0.64 - misclassified as `anti_p`)
  - "“The distance between a place like sderot or arad and tel aviv can be even longer than the distance between tel aviv and new york,” she noted." (Score: 0.78 - misclassified as `pro_p`)
  - "Lapid may seem to be the ultimate tel aviv insider, and at first, it is surprising that she wrote about characters who live on the margins of society, but as you speak to her more, you begin to understand that she can identify with these characters because she also grew up feeling like an outsider." (Score: 0.83 - misclassified as `pro-p`)

- **Anti-Israeli Sentences:**
  - "If i had not been surrounded by five border policemen, i would not have left that protest alive; there was a guy who had already begun swinging his hand in my direction." (Score: 0.70 - misclassified as `neutral`)
  - "Israeli police reported that a 42-year-old man was stabbed at the temple mount compound on tuesday evening and that the red crescent has evacuated him to a hospital, where his death was determined shortly thereafter." (Score: 0.52 - misclassified as `neutral`)
  - "“Really rough feelings,” hapoel tel aviv head coach yossi abukasis said." (Score: 0.67 - misclassified as `pro_p`)
  - "The nation of israel has lost one of its best." (Score: 0.63 - misclassified as `pro_i`)
  - "Muir also asked netanyahu if he took responsibility for the israeli security failure that led to the october 7 attack." (Score: 0.54 - misclassified as `neutral`)

- **Anti-Palestinian Sentences:**
  - "A ceasefire would be a surrender to hamas." (Score: 0.55 - misclassified as `pro_p`)
  - "“There will be no general ceasefire in gaza without the release of our hostages,” he stressed." (Score: 0.82 - misclassified as `pro_p`)
  - "In 2018, fifa fined rajoub $20,000 and banned him from the association for inciting hatred and violence against argentina, which had agreed to play a friendly match in israel." (Score: 0.69 - misclassified as `anti_i`)
  - "I call on the countries of the region to stop iran from harming its sovereignty and residents (Score: 0.36 - misclassified as `neutral`)

**Reasoning:** The model struggles due to insufficient given labels correct classification. Additional work on data preprocessing, labeling and model tuning could improve the results. For example:
  - "The genocide in gaza is reshaping psychic life and political imaginations far beyond palestine" - The sentence explains that the genocide in Gaza is affecting how people think and form political ideas, even outside of Palestine. It was misclassified as `anti_p` because the semantic model first marked it as negative (`NEG`) due to the negative content. Then, because it was about Palestine, it was labeled as `anti-p`. In fact, the sentence is obviously support Palestine.

## Article-Level Analysis

### Article Category Distribution by Newspaper (Counts & Percentages)

---

![Pie-Chart-A-J](charts\\A-J_pie_chart.png)

---

![Pie-Chart-BBC](charts\\BBC_pie_chart.png)

---

![Pie-Chart-J-P](charts\\J-P_pie_chart.png)

---

![Pie-Chart-NY-T](charts\\NY-T_pie_chart.png)

---

![Articles-Counts](images\\articles.png)

---

### Correct Classification
- **Pro-Israeli Articles:**
  - ```text
    ['scotland head coach pedro martinez losa named his squad for the upcoming euro 2025 qualifiers against israel and addressed the media. here are the key points from his press conference:he\'s "really excited" to welcome back forwards kirsty hanson and martha thomas after the pair missed the opening two group games through injury.with five players (maciver, brown, grimshaw, weir and watson) out with acl injuries, martinez losa said the frequent issue of acl injuries in the women\'s game is "multifactorial" but a "big aspect" is the scheduling of games.martinez losa says that international matches are three times more demanding than domestic fixtures and that the football calendar needs to be addressed to protect the players.the head coach says scotland have been "put in a position by uefa" to play against israel and "whether i feel comfortable playing against them or not doesn\'t matter, it is my duty to lead scotland".it is the spaniard\'s "dream to see a full crowd at hampden for a swnt match because scottish fans are the best in the world".', 'call to remove pro-palestine mural from worcester building'] (Score: 0.58)
    ```
    
  - ```text
      ['four goals from martha thomas guided unbeaten scotland to a comprehensive victory over israel that maintains their lead at the top of group b2 in euro 2025 qualifying. the tottenham hotspur striker scored two either side of half-time in scotland\'s second meeting with israel in four days behind closed doors as pedro martinez losa\'s side secured a play-off spot.thomas slotted the opener in budapest, hungary, after another impressive start from the scots before heading in a second on the end of an outstanding team move.her team-mates could have chipped in with a few in between, but the striker settled any nerves with a third following good movement and added a fourth with her head. once the 28-year-old was substituted, chelsea cornet took the reins and emphatically netted her first international goal with a smashed effort late on.serbia\'s impressive 4-0 away to slovakia later in the evening means they remain tied with the scots on points but behind on goal difference. friday nightֳ¢_x0080__x0099_s first-half performance generated heaps of praise due to the forward-thinking play, dominance in the final third and, crucially, goals, which have been a bit sparse for scotland of late.there was hope that could be replicated in hungary and, after a slightly sticky start, scotland met expectations.thomas, who scored the fourth from the spot four days ago, eventually slotted home after breaking away from the defence, but the visitors arguably should have been out of sight already.on her 50th appearance, sophie howardֳ¢_x0080__x0099_s header was cleared off the line, while claire emslie and kirsty hanson ֳ¢_x0080__x0093_ who both scored on friday ֳ¢_x0080__x0093_ smacked the woodwork and emslie was also denied by fortuna rubinֳ¢_x0080__x0099_s strong foot.the scots didnֳ¢_x0080__x0099_t let up and a sharp second seemed to be scored after a bit of a stramash in the six-yard-box. the ball appeared to be in, but the officials were unmoved and, with no goalline technology, play continued.the second did come, through thomas of course, and while she got the final nod, it was all about the well-worked build-up play from captain rachel corsieֳ¢_x0080__x0099_s defence-splitting pass to lisa evansֳ¢_x0080__x0099_ pinpoint cross.thomas squandered a header, but her first international hat-trick was soon complete, courtesy of her knee. and why stop at three? once again, her height proved too difficult to deal with and she rose for a fourth on her best afternoon in a scotland shirt. chances came and went for emslie and cornet too, but the rangers midfielder finally found her opportunity to seal an impressive win on the road for the scots. the double-header against israel sandwiched in the middle of the fixture list was always viewed as a must-win pair of games, with the hope of a good few goals too.scotland completed the task at hand with relative ease, barring a few scares on friday which were handled well by lee gibson in goal.martinez losaֳ¢_x0080__x0099_s side looked back to their old selves. the confidence was no doubt knocked by the poor nations league campaign and the pinatar cup was not as successful on the pitch as some would have hoped.however, going undefeated in the first four group b2 games has allowed the scots to smile again and play some lovely stuff, despite missing key operators.across both games, the front three of hanson, thomas and emslie have particularly impressed, and their link-up play has been joyous. they seem settled and connected, which will be key if next summerֳ¢_x0080__x0099_s euros are eventually reached.with erin cuthbert rested, captain corsie shifted into the midfield and made the position look her own. her natural instinct to sit deep allowed sam kerr to roam forward and influence the top end of the pitch alongside cornet. scotland head coach pedro martinez losa: "we are very happy with the performance, very proud of the team. it was a proper team performance with some circumstances to deal with throughout the game but that\'s what a team is there for."we are more proactive in the final third and martha is a player who can be very effective from crosses and that\'s something we managed to do." scotland have two games left in the group, away to slovakia on 12 july (18:00 bst) before ending the campaign by hosting serbia four days later (18:00).', 'what icc arrest warrants mean for israel, benjamin netanyahu and hamas'] (Score: 0.58)
    ```

- **Pro-Palestinian Articles:**
  - ```text
    ['us students use graduation to stand with palestine', 'protests, messages weaved into commencement addresses and the heckling of guest speakers, including comedian jerry seinfeld are just some of the ways students in the us showed support for palestine during graduation ceremonies in the us.'] (Score: 0.41)
    ```
    
  - ```text
    ['palestinians in rafah express thanks to us university protesters', 'displaced palestinians in gaza are expressing their thanks to student protesters on us college campuses by writing messages of gratitude on their tents in rafah.'] (Score: 0.70)
    ```
    
- **Neutral Articles:**
  - ```text
    ['rough seas for blinken and co. as israel, iran and ukraine cloud g7 meeting'] (Score: 0.41)
    ```
    
  - ```text
    ['netanyahu to send israeli team to washington to discuss rafah plans'] (Score: 0.71)
    ```
    
- **Anti-Israeli Articles:**
  - ```text
    ['the international court of justice called on israel to end its operation in rafah, the southernmost town in gaza.', 'icj rules israel must stop rafah operation, whatג€™s next?', 'the international court of justice has issued a legally binding order for israel to halt its invasion of rafah.']  (Score: 0.79)
    ```
    
  - ```text
    ['thirteen out of 21 people killed by israel in an air strike on the so-called 'safe area' of al-mawasi were civilian women and girls, al jazeera's hind khoudary reported on tuesday.', 'what happened when israel attacked rafah?', 'israel has attacked twice since sunday, killing tens of people in horrific circumstances.'] (Score: 0.76)
    ```
    
- **Anti-Palestinian Articles:**
  - ```text
    ['over 100 pro-palestine protesters arrested at us university', 'us police arrested more than 100 protesters who had set up camp to demonstrate against israel's war on gaza from columbia university's campus in new york.'] (Score: 0.70)
    ```
    
  - ```text
    ['johnson calls to end pro-palestinian protests, including by military means'] (Score: 0.54)
    ```
