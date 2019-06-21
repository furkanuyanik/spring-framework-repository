# spring-framework-repository
How to use Repository in Spring Framework?

# Create Models named Customer and CustomerType

  @Entity
  @AllArgsConstructor
  @NoArgsConstructor
  @Data
  public class Customer {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    public int Id;
    public String customerName;
    
    @OneToOne
    @JoinColumn(name = "customerType", referencedColumnName = "id")
    public CustomerType customerType;
  }
  
  @Entity
  @AllArgsConstructor
  @NoArgsConstructor
  @Data
  public class CustomerType {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    public int Id;
    public String customerTypeName;
  }

# Create Repository
  @Repository
  public interface CustomerRepository extends CrudRepository<Customer, Integer> {
    // ...
  }
  
# Write Function in CustomerRepository
