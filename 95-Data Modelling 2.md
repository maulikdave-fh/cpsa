## Products & Sums in Data Modelling
1. "Product" and "Sum" type describe the structure of entities.
2. The concept of products and sums comes from Functional Programming and type theory

### "Product" Type
1. An entity with fixed number of required attributes / fields
2. Represents "AND" relationship between multiple values together
3. Other names;
   - Record
   - Struct
   - Data class
   - Tuple
  
### "Sum" Type
1. Represents choice between multiple values
2. Creates "OR" relationship
3. Other names;
   - Discriminated union
   - Disjoint union
   - Union
   - Mixed data
  
## Example
![Online store!](/store1.png)

Purchase Txn Implementation with Java
```
  public record PurchaseTransaction(int userId, int productId, int quantity, PaymentType paymentType) {
      sealed interface PaymentType permits CreditCard, PayPal  {}
      record CreditCard(String PAN, int securityCode, LocalDate expiryDate) implements PaymentType {}
      record PayPal(String email) implements PaymentType {} 
  }
```
