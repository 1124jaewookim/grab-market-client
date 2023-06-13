# CATCH MARKET

## Team Information

- This project has been built by Team 11.
- Team Members:
  - Jaewoo Kim (https://1124jaewookim.github.io)
  - Hojoon Lee ([Member 2 Website])
  - Jey Kang ([Member 3 Website])
  - HYEBIN JIN (straybuilds.github.io)

## Problem Definition (250 words)

Advances in machine learning technology have revolutionized many fields, and the fashion industry is no exception. One such innovation is the emergence of a new web service that uses machine learning algorithms to identify photos of people wearing clothing or illustrations of fashion designs from uploaded images.

The premise of this service is both simple and ingenious. Users can upload a photo of a person wearing an outfit they find attractive or an illustration of a clothing design they envision. An underlying machine learning model, trained on a large dataset of fashion images and their associated metadata, analyzes the uploaded image. By identifying key features such as color, pattern, fabric, style, and cut, it matches clothing items in the image to similar items in the database.

However, the usefulness of this web service extends beyond simply identifying matching clothing items. Once the AI has made a selection, it provides the user with a direct link to an e-commerce website where they can purchase the matching or similar clothing item. This feature saves users the tedious process of searching through numerous online stores to find the item they want.

The service leverages the power of machine learning to bridge the gap between the fashion items you're looking for and the ones you'll actually buy. Whether it's discovering a great outfit from a stranger or bringing a creative fashion sketch to life, this web service can change the way people explore and experience fashion.

## System Design (500 words)

In our system, we differentiate between client pages and server pages. The client pages are implemented using REACT and NodeJS, and similarly, the server pages are also implemented using REACT and NodeJS as a base. The client pages do not have any internally stored data; instead, they communicate with the server pages to retrieve information, including banners and other data. The server serves as a database and accumulates the necessary information for the service. We deployed the client using a web service called Vercel and the database using another web service called Fly.io.
When the client page is executed, it automatically fetches the past product search information stored in the database and displays it in a photocard format. When a user wants to perform a new search, they enter the upload page, where the user provides information about the new product to search for (photo, user name, product title, price). This information is then uploaded to the server. Once the upload is complete, the client page returns to its initial state, and during the process of fetching the past product search information from the database, the recently searched results are also retrieved. Storing all the data on the server when performing a new search is done to allow other users to see all previous results when they access the client page. When a photocard is clicked on the main screen, the corresponding information opens in a new window. At the bottom of this window, there is a link to recommended products, which leads to the product purchase page.
The server has multiple roles, with the primary one being the database functionality. It uses SQLite to store new data in a row-based manner. When the client page sends new information through a POST request called "products," the server stores the product ID, name, price, search time, seller, image URL, and availability based on the provided information. To reduce the server's data load, images are not encoded as part of the request; instead, a static file folder is created, and the corresponding URL is used.
Furthermore, for each search request, the server determines which existing product in the database is most similar to each search product and generates a recommendation list. Initially, a pre-trained TensorFlow.js MobileNet model is used to determine the class (e.g., shirt, jeans) of each product. Then, among the products of the same class in the database, the one with the highest similarity is considered as the recommended result. Initially, the plan was to incorporate Python for additional tasks. However, difficulties in deploying the server using AWS Lambda due to Docker Desktop issues and network limitations within the university led to exploring alternatives. Our site was deployed using external services like Vercel and Fly.io, making it impossible to communicate with the server PC using FASTAPI over an external network. Therefore, the intended implementation with Python for classifying products and using models like ResNet50 for feature extraction and similarity measurement using MSE or cosine similarity could not be realized. Additionally, with the availability of PyTorch, various additional functionalities were planned for implementation if needed.

## Machine Learning Component (300 words)

We use ML components to construct our recommendation API. If a consumer uploads an image similar to the clothes they want to buy on the website, our Catch Market encodes and classifies the image and displays similar images at the bottom of the web interface. As an encoder for our recommendation model, we select MobileNet. MobileNet is a convolutional neural network (CNN) architecture that is specifically designed for efficient mobile and embedded vision applications. With its affordable accuracy and low latency, it can be used effectively in recommendation systems for shopping websites. Below illustrate several strengths of the MobileNet for a recommendation API in a shopping website.

Efficient and Lightweight: MobileNet is known for its compact size and low computational requirements compared to other deep learning models. This is important for recommendation systems as they often need to process large amounts of data in real-time. MobileNet's efficiency allows for faster inference and lower resource consumption, making it suitable for deployment in web applications and mobile devices.

Good Performance: Despite its compact size, MobileNet still performs well in terms of accuracy. It achieves a good balance between model size and predictive performance. MobileNet's architecture is designed to extract meaningful features from images, which can be used to understand product attributes and user preferences in a shopping context.

Real-time Recommendations: MobileNet's efficiency allows for quick inference, enabling real-time recommendations in a shopping website. This is crucial as users expect fast and personalized recommendations while browsing through products. MobileNet can process images efficiently, extract relevant features, and provide recommendations promptly, enhancing the user experience.

Furthermore, between product class-based recommendation and feature-based recommendation, we chose class-based recommendation ML systems with careful consideration for two reasons. First, It can use domain specific knowledge of a certain class. Class-based recommendation API can leverage domain-specific knowledge and expertise to provide more accurate and relevant recommendations. By understanding the characteristics, attributes, and relationships within a product class, the API can make informed recommendations that align with users' interests. Second, Recommending items from the same product class allows users to discover new products within the categories they are interested in. Users might be looking for alternatives, variations, or complementary items related to a specific product class. By suggesting items from the same category, users can explore a wider range of options within their preferred domain.

## System Evaluation (500 words)

The key component of our system evaluation contains several steps. First, we sampled about 100 images from data crawled from several main shopping sites and used them as test images for the recommendation API. After the sampling step, the class of each image was organized in a table format by passing through the aforementioned MobileNet, which is the backbone of the recommendation model.

Then, our team members shared the outputs of the organized table, and manually verified whether the recommendation model correctly classified the images. By repeatedly performing this verification process, the database and our crawled data were refined with images that can be correctly classified by the model, which enabled us to provide a high-quality recommendation system.

Moreover, we also conducted a survey of potential consumers of our Catch Market to find out what their acceptable latency rate was. Using the two peer evaluation opportunities provided in the Data Engineering class, the opinions of about 15 users were collected, and the latency of the recommendation API that they found acceptable was about 3.4 seconds. By considering both the average latency consumers wanted and the latency provided by other benchmarked models, we select the backbone of our recommendation system.

Finally, we collected offline comprehensive feedback and evaluation of our systems from potential users. Since such evaluation plays a key role in determining user satisfaction with the web service, we thought this is the most important thing in our project. We actively gathered feedback from users through surveys and interviews and asked users about their satisfaction with the recommendations received, whether they found them helpful, and if they felt the recommendations were aligned with their preferences. Through the above user feedback and evaluation, we notice that they want at least one product displayed in the recommendation interface. Also, they want an actual website where they can buy the recommended products. Therefore, to reflect the opinions, the algorithm and the database of the shopping website were modified, and their needs could be satisfied.

## Application Demonstration (300 words)

[Include visuals showcasing the main features of your application, along with justifications for core interface decisions. Provide instructions on how to use the application.]

## Reflection (400 words)

[Provide a post-mortem on the project, including what worked, what didn't work, improvements for the future, and plans to move forward.]

## Broader Impacts (250 words)

[Discuss the intended and unintended uses of your application and associated harms. Reflect on design decisions to mitigate unintended use.]

---

**Deliverables**

Please find the following deliverables for our project:

1. Code, data, and associated materials used for the project:

   - [GitHub Repo Link]

2. Final Report:
   - [Link to the Blog Post or ZIP file containing HTML report]

---

Thank you for reviewing our project report. Should you have any questions or require further information, please don't hesitate to contact us.
