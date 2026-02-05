
Running on public URL: https://4e3650eebc8a9bbee2.gradio.live

================================ ABOUT PROJECT  =====================================================================
 
 Enhanced Medical Note Retrieval for Improved Clinical Decision-Making
Scenario: A healthcare system allows doctors to search through a large dataset of medical notes to find relevant patient information.

Application: After an initial list of relevant notes is generated from a search query, a reranker can fine-tune the order by considering factors such as the specificity of the medical conditions mentioned, and the relevance to the patient's current symptoms or treatment plan. This ensures that the most critical and contextually relevant notes are presented first, aiding in quicker and more accurate clinical decision-making.

================================ ARCHITECRURE  =====================================================================

Steps in This Agent:
Load Libraries
Load Small Documents Object
Execute Reranking Model
Show Results
Create Index
Upsert Sample Data
Embed Query
Execute Search
View Results
Rerank Results

The main dataset we will be using consists of randomly generated doctor’s notes sample data. The original JSON data has been embedded into vectors, which we will load into Pinecone.

================================ OUTPUT  =====================================================================

================================       Results before from RAG     ==================================================

Question: 'what if my patient has leg pain'

Results:
   1. ID: P0100
      Score: 0.518160701
      Metadata: {'advice': 'over-the-counter pain relief, stretching', 'symptoms': 'muscle pain'}

   2. ID: P047
      Score: 0.501062632
      Metadata: {'symptoms': 'back pain', 'treatment': 'physical therapy'}

   3. ID: P095
      Score: 0.501062632
      Metadata: {'symptoms': 'back pain', 'treatment': 'physical therapy'}

   4. ID: P007
      Score: 0.459310442
      Metadata: {'surgery': 'knee arthroscopy', 'symptoms': 'pain, swelling', 'treatment': 'physical therapy'}

   5. ID: P028
      Score: 0.445996523
      Metadata: {'condition': 'knee pain', 'referral': 'orthopedics'}

   6. ID: P059
      Score: 0.430181175
      Metadata: {'symptoms': 'joint pain', 'treatment': 'NSAIDs, rest'}

   7. ID: P020
      Score: 0.424475789
      Metadata: {'condition': 'sprained ankle', 'tests': 'X-ray'}

   8. ID: P068
      Score: 0.41390565
      Metadata: {'condition': 'broken arm', 'treatment': 'cast'}

   9. ID: P044
      Score: 0.407784969
      Metadata: {'condition': 'dehydration', 'treatment': 'IV fluids'}

  10. ID: P092
      Score: 0.407784969
      Metadata: {'condition': 'dehydration', 'treatment': 'IV fluids'}


================================       RERANKED results from RAG     ==================================================


Question: 'what if my patient had knee surgery'

Reranked Results:
   1. ID: P007
      Score: 0.18184364
      Reranking Field: surgery: knee arthroscopy; symptoms: pain, swelling; treatment: physical therapy

   2. ID: P028
      Score: 0.0054905633
      Reranking Field: condition: knee pain; referral: orthopedics

   3. ID: P059
      Score: 0.0027900378
      Reranking Field: symptoms: joint pain; treatment: NSAIDs, rest

   4. ID: P095
      Score: 0.0017891593
      Reranking Field: symptoms: back pain; treatment: physical therapy

================================       LLM Response:  W/O RAG       ==================================================


Knee pain is a common complaint that can be caused by a variety of factors. Here are some possible causes and considerations:

**Common causes of knee pain:**

1. **Osteoarthritis**: Wear and tear on the joint cartilage, often due to age, obesity, or previous injuries.
2. **Ligament sprains**: Injuries to the ligaments that connect the bones in the knee, such as the anterior cruciate ligament (ACL) or medial collateral ligament (MCL).
3. **Meniscal tears**: Tears in the cartilage that cushions the joint, often caused by sudden twisting or bending.
4. **Tendinitis**: Inflammation of the tendons that connect muscles to bones, such as the patellar tendon.
5. **Bursitis**: Inflammation of the fluid-filled sacs that cushion the joint, such as the prepatellar bursa.
6. **Patellofemoral pain syndrome**: Pain in the front of the knee, often due to poor tracking of the kneecap (patella).
7. **Referred pain**: Pain that originates from other areas, such as the hip or lower back, and is referred to the knee.

**Questions to ask your patient:**

1. **Location of pain**: Where is the pain located? Is it in the front, back, or side of the knee?
2. **Duration of pain**: How long have you been experiencing knee pain?
3. **Severity of pain**: How would you rate your pain on a scale of 1-10?
4. **Activities that exacerbate pain**: What activities make your pain worse? (e.g., running, jumping, climbing stairs)
5. **Activities that relieve pain**: What activities make your pain better? (e.g., rest, ice, stretching)
6. **Previous injuries or surgeries**: Have you had any previous knee injuries or surgeries?
7. **Medical history**: Do you have any underlying medical conditions, such as diabetes or rheumatoid arthritis?

**Physical examination:**

1. **Inspection**: Observe the knee for any swelling, redness, or deformity.
2. **Palpation**: Feel the knee joint and surrounding tissues for tenderness or warmth.
3. **Range of motion**: Assess the knee's range of motion, including flexion, extension, and rotation.
4. **Special tests**: Perform special tests, such as the McMurray test for meniscal tears or the Lachman test for ACL injuries.

**Diagnostic tests:**

1. **X-rays**: To rule out fractures or osteoarthritis.
2. **MRI**: To evaluate soft tissue injuries, such as ligament sprains or meniscal tears.
3. **Ultrasound**: To evaluate tendon or bursa inflammation.

**Treatment options:**

1. **Conservative management**: Rest, ice, compression, elevation (RICE), physical therapy, and pain management with medication.
2. **Injections**: Corticosteroid or platelet-rich plasma (PRP) injections to reduce inflammation and promote healing.
3. **Surgery**: Arthroscopy, ligament reconstruction, or joint replacement surgery, depending on the underlying cause and severity of the condition.

Remember to always consult with a healthcare professional for an accurate diagnosis and treatment plan.
================================       LLM Response:  WITH RAG       ==================================================


Based on the provided medical notes, the most relevant information for a patient with knee pain is:

1. Document P007, which mentions "symptoms: pain, swelling" and "surgery: knee arthroscopy" with a score of 0.18184364. This suggests that the patient may have undergone knee arthroscopy and is experiencing pain and swelling, which is relevant to their current symptom of knee pain.
2. Document P028, which mentions "condition: knee pain" and "referral: orthopedics" with a score of 0.0054905633. This directly mentions knee pain as a condition, which is highly relevant to the patient's current symptom.

The other documents (P059 and P095) are less relevant to the patient's knee pain, as they mention more general symptoms (joint pain and back pain, respectively) and do not specifically address knee pain.

Therefore, based on the medical notes, it is likely that the patient's knee pain is related to a previous knee arthroscopy (as mentioned in P007) or is a condition that may require referral to an orthopedic specialist (as mentioned in P028). The treatment plan may involve physical therapy (mentioned in P007) or NSAIDs and rest (mentioned in P059, although this is less relevant).