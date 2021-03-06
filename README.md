# spring-framework-repository

# 1. Create Models named Customer and CustomerType
  
    @Entity
    @AllArgsConstructor
    @NoArgsConstructor
    @Data
    public class Customer {
      @Id
      @GeneratedValue(strategy = GenerationType.IDENTITY)
      public int id;
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
      public int id;
      public String customerTypeName;
    }

# 2. Create Repository

    @Repository
    public interface CustomerRepository extends CrudRepository<Customer, Integer> {
      // ...
    }
  
# 3. Write Function in CustomerRepository

  ## WHERE CustomerName = "Furkan"
     public List<Tunnel> findByCustomerName(String customerName);
     
  ## WHERE CustomerName = "Furkan" AND CustomerType.CustomerTypeId = 1
     public List<Tunnel> findByCustomerNameAndCustomerTypeId(String customerName, int customerType);
     
  ## WHERE CustomerName = "Furkan" AND CustomerType.CustomerTypeId = 1
     public List<Tunnel> findByCustomerNameAndCustomerType(String customerName, CustomerType customerType);
     
  ## SELECT * FROM Customer WHERE CustomerType = XXX
     @Query("SELECT t FROM Customer t WHERE t.customerType = :customerType")
     Optional<Iterable<Customer>> select(@Param("customerType") Optional<CustomerType> customerType);
