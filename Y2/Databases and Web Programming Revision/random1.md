
```
entity Car {
	make String
}
```

=>

```
entity Car {
	make String,
	model String required,
	vin Int unique, minlength(17)
	modelYear Integer required min(1900),

	}
```


v2/products?-price,+name

Year is a reserved field! cant use it! will error!

- Getters & Setters all automatically created*

- curl `-x GET` https::/website.com/api/cars

curl -X POST "https://localhost/api/cars " \
-H Content-Type: `application/json` \
-d'{"make":Toyota","model":"Corolla","vin":"123413524","year":2015}'

```
entity Employee {
	name String required,
	department Department,
	team Team 
}

enum Department { HR, ENGINEERING, SALES}

entity Team {
	name String required unique
}

relationship ManyToOne{
Employee{team} to Team{team}
}
```


7
```
entity UserProfile {
	bio TextBlob,
	profilePicture ImageBlob,
	user User
}

relationship OneToOne{
	UserProfile{user} to User **withBuiltInEntity**
}

```

