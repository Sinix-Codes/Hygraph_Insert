**Inserting Data into Hygraph**

Hygraph offers multiple methods for data insertion:

* **Hygraph Management UI:** The user-friendly UI allows you to create content entries directly within the Hygraph dashboard. Simply select a model, click "Create Entry," and populate the fields with your desired content.
* **GraphQL Mutations:** Hygraph leverages GraphQL mutations for programmatic data insertion. You can utilize various tools like GraphQL clients or SDKs to execute mutations.

**Example: Inserting a Product using GraphQL**

Here's an example mutation (using JavaScript syntax) to create a new product:

```javascript
const { gql, GraphQLClient } = require('graphql-request');

const mutation = gql`
  mutation createProduct($title: String!, $description: String!, $price: Float!) {
    createProduct(data: { title: $title, description: $description, price: $price }) {
      id
      title
    }
  }
`;

const client = new GraphQLClient('[YOUR_HYGRAPH_CONTENT_API_URL]'); // Replace with your actual URL

const data = {
  title: 'Awesome T-Shirt',
  description: 'A comfortable and stylish T-shirt for everyday wear.',
  price: 29.99,
};

client.mutate(mutation, data)
  .then(response => console.log('Product created:', response.createProduct))
  .catch(error => console.error(error));
```