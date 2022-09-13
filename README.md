# spring-boot-learning
This projects contains theory and some examples of Spring Boot

spring-data-jpa

The save() itself contains both create and update operation.

What is behind the save() method.

Firstly, let's see the extend/implement hierarchy of the CrudRepository<T,ID>

Ok, let's check the save() implementation at SimpleJpaRepository<T, ID>,

@Transactional
public <S extends T> S save(S entity) {

    if (entityInformation.isNew(entity)) {
        em.persist(entity);
        return entity;
    } else {
        return em.merge(entity);
    }
}
As you can see, it will check whether the ID is existed or not firstly,
if the entity is already there, only update will happen by merge(entity) method and 
if else, a new record is inserted by persist(entity) method.
