# SQL Practice

### Hospital DB

<img src='/img/hospital-der.png' />

###### 1. Show first name, last name, and gender of patients whose gender is 'M'

<details>
  <summary>Solution</summary>
  <p>

```sql
SELECT first_name, last_name, gender FROM patients
WHERE gender = 'M'
```

  </p>
</details>

###### 2. Show first name and last name of patients who does not have allergies. (null)

<details>
  <summary>Solution</summary>
  <p>

```sql
SELECT first_name, last_name FROM patients
WHERE allergies IS NULL
```

  </p>
</details>

###### 3. Show first name of patients that start with the letter 'C'

<details>
  <summary>Solution</summary>
  <p>

```sql
SELECT first_name FROM patients
WHERE first_name LIKE 'C%'
```

  </p>
</details>

###### 4. Show first name and last name of patients that weight within the range of 100 to 120 (inclusive)

<details>
  <summary>Solution</summary>
  <p>

```sql
SELECT first_name, last_name FROM patients
WHERE weight BETWEEN 100 AND 120
```

  </p>
</details>

###### 5. Update the patients table for the allergies column. If the patient's allergies is null then replace it with 'NKA'

<details>
  <summary>Solution</summary>
  <p>

```sql
UPDATE patients
SET allergies = 'NKA'
WHERE allergies IS NULL
```

  </p>
</details>

###### 6. Show first name and last name concatinated into one column to show their full name.

<details>
  <summary>Solution</summary>
  <p>

```sql
SELECT CONCAT(first_name,' ', last_name) FROM patients
```

  </p>
</details>

###### 7. Show first name, last name, and the full province name of each patient.

<details>
  <summary>Solution</summary>
  <p>

```sql
SELECT first_name, last_name, province_name FROM patients p
INNER JOIN province_names pn
ON pn.province_id = p.province_id
```

  </p>
</details>

###### 8. Show how many patients have a birth_date with 2010 as the birth year.

<details>
  <summary>Solution</summary>
  <p>

```sql
SELECT COUNT(*) FROM patients
WHERE YEAR(birth_date) = 2010
```

  </p>
</details>

###### 9. Show the first_name, last_name, and height of the patient with the greatest height.

<details>
  <summary>Solution</summary>
  <p>

```sql
SELECT first_name, last_name, MAX(height) FROM patients
```

  </p>
</details>

###### 10. Show all columns for patients who have one of the following patient_ids: 1,45,534,879,1000

<details>
  <summary>Solution</summary>
  <p>

```sql
SELECT * FROM patients
WHERE patient_id IN (1,45,534,879,1000)
```

  </p>
</details>
