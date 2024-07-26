# SQL Practice

### Hospital DB

<img src='/img/hospital-der.png' />

---

#### Easy

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

###### 11. Show the total number of admissions

<details>
  <summary>Solution</summary>
  <p>

```sql
SELECT COUNT(*) FROM admissions
```

  </p>
</details>

###### 12. Show all the columns from admissions where the patient was admitted and discharged on the same day.

<details>
  <summary>Solution</summary>
  <p>

```sql
SELECT * FROM admissions
WHERE admission_date = discharge_date
```

  </p>
</details>

###### 13. Show the patient id and the total number of admissions for patient_id 579.

<details>
  <summary>Solution</summary>
  <p>

```sql
SELECT patient_id, count(*) AS total_admissions FROM admissions
WHERE patient_id = 579
```

  </p>
</details>

###### 14. Based on the cities that our patients live in, show unique cities that are in province_id 'NS'?

<details>
  <summary>Solution</summary>
  <p>

```sql
SELECT DISTINCT city FROM patients
WHERE province_id = 'NS'
```

  </p>
</details>

###### 15. Write a query to find the first_name, last name and birth date of patients who has height greater than 160 and weight greater than 70

<details>
  <summary>Solution</summary>
  <p>

```sql
SELECT first_name, last_name, birth_date FROM patients
WHERE height > 160 AND weight > 70
```

  </p>
</details>

###### 16. Write a query to find list of patients first_name, last_name, and allergies where allergies are not null and are from the city of 'Hamilton'

<details>
  <summary>Solution</summary>
  <p>

```sql
SELECT first_name, last_name, allergies FROM patients
WHERE allergies IS NOT NULL AND city = 'Hamilton'
```

  </p>
</details>

---

#### Medium

###### 1. Show unique birth years from patients and order them by ascending.

<details>
  <summary>Solution</summary>
  <p>

```sql
SELECT DISTINCT YEAR(birth_date) FROM patients
ORDER BY birth_date ASC
```

  </p>
</details>

###### 2. Show unique first names from the patients table which only occurs once in the list.

<details>
  <summary>Solution</summary>
  <p>

```sql
SELECT first_name FROM patients
GROUP BY first_name
HAVING COUNT(first_name) = 1
```

  </p>
</details>

###### 3. Show patient_id and first_name from patients where their first_name start and ends with 's' and is at least 6 characters long.

<details>
  <summary>Solution</summary>
  <p>

```sql
SELECT patient_id,first_name FROM patients
WHERE first_name LIKE 's%s' AND LEN(first_name) >= 6
---
SELECT patient_id,first_name FROM patients
WHERE first_name LIKE 's____%s'
```

  </p>
</details>

###### 4. Show patient_id, first_name, last_name from patients whos diagnosis is 'Dementia'. Primary diagnosis is stored in the admissions table.

<details>
  <summary>Solution</summary>
  <p>

```sql
SELECT p.patient_id, first_name, last_name FROM patients p
INNER JOIN admissions a
ON p.patient_id = a.patient_id
WHERE diagnosis = 'Dementia'
```

  </p>
</details>

###### 5. Display every patient's first_name. Order the list by the length of each name and then by alphabetically.

<details>
  <summary>Solution</summary>
  <p>

```sql
SELECT first_name FROM patients
ORDER BY LEN(first_name), first_name
```

  </p>
</details>

###### 6. Show the total amount of male patients and the total amount of female patients in the patients table. Display the two results in the same row.

<details>
  <summary>Solution</summary>
  <p>

```sql
SELECT
  SUM(gender = 'M') AS Male,
  SUM(gender = 'F') AS Female
FROM patients
---
SELECT
  SUM(CASE WHEN gender = 'M' THEN 1 END) AS male_count,
  SUM(CASE WHEN gender = 'F' THEN 1 END) AS female_count
FROM patients;
```

  </p>
</details>

###### 7. Show first and last name, allergies from patients which have allergies to either 'Penicillin' or 'Morphine'. Show results ordered ascending by allergies then by first_name then by last_name.

<details>
  <summary>Solution</summary>
  <p>

```sql
SELECT first_name, last_name, allergies FROM patients
WHERE allergies IN ('Penicillin','Morphine')
ORDER BY allergies, first_name, last_name
```

  </p>
</details>

###### 8. Show patient_id, diagnosis from admissions. Find patients admitted multiple times for the same diagnosis.

<details>
  <summary>Solution</summary>
  <p>

```sql
SELECT patient_id, diagnosis FROM admissions
GROUP BY patient_id,diagnosis
HAVING count(*) > 1
```

  </p>
</details>

###### 9. Show the city and the total number of patients in the city. Order from most to least patients and then by city name ascending.

<details>
  <summary>Solution</summary>
  <p>

```sql
SELECT city, COUNT(*) AS total_patients FROM patients
GROUP BY city
ORDER BY total_patients DESC, city ASC
```

  </p>
</details>

###### 10. Show first name, last name and role of every person that is either patient or doctor. The roles are either "Patient" or "Doctor"

<details>
  <summary>Solution</summary>
  <p>

```sql
SELECT first_name, last_name, 'Patient' AS role
FROM patients
UNION ALL
SELECT first_name, last_name, 'Doctor' AS role
FROM doctors
```

  </p>
</details>

###### 11. Show all allergies ordered by popularity. Remove NULL values from query.

<details>
  <summary>Solution</summary>
  <p>

```sql
SELECT allergies, COUNT(*) AS popularity FROM patients
WHERE allergies IS NOT NULL
GROUP BY allergies
ORDER BY popularity DESC
```

  </p>
</details>

###### 12. Show all patient's first_name, last_name, and birth_date who were born in the 1970s decade. Sort the list starting from the earliest birth_date.

<details>
  <summary>Solution</summary>
  <p>

```sql
SELECT first_name, last_name, birth_date FROM patients
WHERE YEAR(birth_date) BETWEEN 1970 AND 1979
ORDER BY birth_date
```

  </p>
</details>

###### 13. We want to display each patient's full name in a single column. Their last_name in all upper letters must appear first, then first_name in all lower case letters. Separate the last_name and first_name with a comma. Order the list by the first_name in decending order.

<details>
  <summary>Solution</summary>
  <p>

```sql
SELECT concat(upper(last_name),',', lower(first_name)) AS full_name
FROM patients
ORDER BY first_name DESC
```

  </p>
</details>

###### 14. Show the province_id(s), sum of height; where the total sum of its patient's height is greater than or equal to 7,000.

<details>
  <summary>Solution</summary>
  <p>

```sql
SELECT province_id, SUM(height) AS max_height
FROM patients
GROUP BY province_id
HAVING max_height >= 7000
```

  </p>
</details>

###### 15. Show the difference between the largest weight and smallest weight for patients with the last name 'Maroni'.

<details>
  <summary>Solution</summary>
  <p>

```sql
SELECT (MAX(weight) - MIN(weight)) AS diff_weight
FROM patients
WHERE last_name = 'Maroni'
```

  </p>
</details>

###### 16. Show all of the days of the month (1-31) and how many admission_dates occurred on that day. Sort by the day with most admissions to least admissions.

<details>
  <summary>Solution</summary>
  <p>

```sql
SELECT DAY(admission_date) AS admissions_day, count(*) admissions_for_day
FROM admissions
GROUP BY admissions_day
ORDER BY admissions_for_day DESC
```

  </p>
</details>

###### 17. Show all columns for patient_id 542's most recent admission_date.

<details>
  <summary>Solution</summary>
  <p>

```sql
SELECT * FROM admissions
GROUP BY patient_id
HAVING patient_id = 542 AND MAX(admission_date)
---
SELECT * FROM admissions
WHERE patient_id = 542
ORDER BY admission_date DESC
LIMIT 1
```

  </p>
</details>

###### 18. Show patient_id, attending_doctor_id, and diagnosis for admissions that match one of the two criteria:

1. patient_id is an odd number and attending_doctor_id is either 1, 5, or 19.
2. attending_doctor_id contains a 2 and the length of patient_id is 3 characters.

<details>
  <summary>Solution</summary>
  <p>

```sql
SELECT patient_id, attending_doctor_id, diagnosis
FROM admissions
WHERE MOD(patient_id,2) != 0 AND attending_doctor_id IN(1,5,19)
OR
attending_doctor_id LIKE '%2%' AND LEN(patient_id) = 3
```

  </p>
</details>

###### 19. Show first_name, last_name, and the total number of admissions attended for each doctor. Every admission has been attended by a doctor.

<details>
  <summary>Solution</summary>
  <p>

```sql
SELECT d.first_name, d.last_name, COUNT(*) AS total_admissions
FROM admissions
INNER JOIN doctors d
ON attending_doctor_id = doctor_id
GROUP BY d.first_name, d.last_name
```

  </p>
</details>

###### 20. For each doctor, display their id, full name, and the first and last admission date they attended.

<details>
  <summary>Solution</summary>
  <p>

```sql
SELECT d.doctor_id, CONCAT(d.first_name,' ', d.last_name) AS full_name, MIN(admission_date) AS first_admission, MAX(admission_date) AS last_admission
FROM admissions
INNER JOIN doctors d
ON attending_doctor_id = doctor_id
GROUP BY doctor_id
```

  </p>
</details>

###### 21. Display the total amount of patients for each province. Order by descending.

<details>
  <summary>Solution</summary>
  <p>

```sql
SELECT province_name, COUNT(*) AS total_patients FROM patients p
INNER JOIN province_names pn
ON p.province_id = pn.province_id
GROUP BY province_name
ORDER BY total_patients DESC
```

  </p>
</details>

###### 22. For every admission, display the patient's full name, their admission diagnosis, and their doctor's full name who diagnosed their problem.

<details>
  <summary>Solution</summary>
  <p>

```sql
SELECT CONCAT(p.first_name,' ', p.last_name) AS full_name_patient, diagnosis, CONCAT(d.first_name,' ', d.last_name) AS full_name_doctor
FROM patients p
INNER JOIN admissions a
ON p.patient_id = a.patient_id
INNER JOIN doctors d
ON a.attending_doctor_id = d.doctor_id
```

  </p>
</details>

###### 23. Display the first name, last name and number of duplicate patients based on their first name and last name.

<details>
  <summary>Solution</summary>
  <p>

```sql
SELECT first_name, last_name, COUNT(*) AS duplicates
FROM patients
GROUP BY first_name, last_name
HAVING duplicates > 1
```

  </p>
</details>

###### 24. Display patient's full name, height in the units feet rounded to 1 decimal, weight in the unit pounds rounded to 0 decimals, birth_date, gender non abbreviated.

_Convert CM to feet by dividing by 30.48.
Convert KG to pounds by multiplying by 2.205._

<details>
  <summary>Solution</summary>
  <p>

```sql
SELECT CONCAT(first_name,' ',last_name),
ROUND(height/30.48,1) AS height_ft,
ROUND(weight*2.205) AS weight_lb,
birth_date,
CASE
WHEN gender = 'M' THEN 'Male'
WHEN gender = 'F' THEN 'Female'
END AS gender
FROM patients
```

  </p>
</details>

###### 25. Show patient_id, first_name, last_name from patients whose does not have any records in the admissions table. (Their patient_id does not exist in any admissions.patient_id rows.)

<details>
  <summary>Solution</summary>
  <p>

```sql
SELECT p.patient_id, first_name, last_name FROM patients p
LEFT JOIN admissions a
ON p.patient_id = a.patient_id
WHERE a.patient_id IS NULL
----
SELECT p.patient_id, first_name, last_name
FROM patients p
WHERE p.patient_id NOT IN (
    SELECT a.patient_id
    FROM admissions a
  )
```

  </p>
</details>

#### Hard

###### 1. Show all of the patients grouped into weight groups. Show the total amount of patients in each weight group. Order the list by the weight group decending.

_For example, if they weight 100 to 109 they are placed in the 100 weight group, 110-119 = 110 weight group, etc._

<details>
  <summary>Solution</summary>
  <p>

```sql
SELECT
COUNT(*) AS total_patients,
FLOOR(weight / 10) * 10 AS weight_range
FROM patients
GROUP BY weight_range
ORDER BY weight_range DESC
```

  </p>
</details>

###### 2. Show patient_id, weight, height, isObese from the patients table.

_Display isObese as a boolean 0 or 1._
_Obese is defined as weight(kg)/(height(m)2) >= 30._
_weight is in units kg._
_height is in units cm._

<details>
  <summary>Solution</summary>
  <p>

```sql
SELECT patient_id, weight, height,
CASE
	WHEN weight/(POWER(height,2)/10000) >= 30
    THEN 1
    ELSE 0
END AS isObese
FROM patients
```

  </p>
</details>

###### 3. Show patient_id, first_name, last_name, and attending doctor's specialty.Show only the patients who has a diagnosis as 'Epilepsy' and the doctor's first name is 'Lisa'

_Check patients, admissions, and doctors tables for required information._

<details>
  <summary>Solution</summary>
  <p>

```sql
SELECT p.patient_id, p.first_name, p.last_name, d.specialty
FROM patients p
INNER JOIN admissions a
USING (patient_id)
INNER JOIN doctors d
ON a.attending_doctor_id = d.doctor_id
WHERE d.first_name = 'Lisa' AND diagnosis = 'Epilepsy'
```

  </p>
</details>

###### 4. All patients who have gone through admissions, can see their medical documents on our site. Those patients are given a temporary password after their first admission. Show the patient_id and temp_password.

The password must be the following, in order:

1. patient_id
2. the numerical length of patient's last_name
3. year of patient's birth_date\*

<details>
  <summary>Solution</summary>
  <p>

```sql
SELECT patient_id,
CONCAT(patient_id,LEN(last_name),YEAR(birth_date)) AS temp_password
FROM patients
WHERE patient_id IN (
  SELECT patient_id FROM admissions
	GROUP BY patient_id
  )
----
SELECT p.patient_id,
CONCAT(p.patient_id,LEN(last_name),YEAR(birth_date)) AS temp_password
FROM patients p
INNER JOIN admissions USING(patient_id)
GROUP BY patient_id
```

  </p>
</details>

###### 5. Each admission costs `$50` for patients without insurance, and `$10` for patients with insurance. All patients with an even patient_id have insurance.

###### Give each patient a 'Yes' if they have insurance, and a 'No' if they don't have insurance. Add up the admission_total cost for each has_insurance group.

<details>
  <summary>Solution</summary>
  <p>

```sql
SELECT
  CASE
    WHEN patient_id % 2 = 0 THEN 'Yes'ELSE 'No'
  END AS has_insurance,
  SUM(
    CASE
      WHEN patient_id % 2 = 0 THEN 10 ELSE 50
    END
    ) AS admissio_total
FROM admissions
GROUP BY has_insurance

----

SELECT
  has_insurance,
  CASE
    WHEN has_insurance = 'Yes' THEN COUNT(has_insurance) * 10
    ELSE COUNT(has_insurance) * 50
  END AS cost_after_insurance
FROM (
    SELECT
      CASE
        WHEN patient_id % 2 = 0 THEN 'Yes'
        ELSE 'No'
      END AS has_insurance
    FROM admissions
  )
GROUP BY has_insurance

----

SELECT has_insurance,SUM(admission_cost) AS admission_total
FROM
(
   SELECT patient_id,
   CASE WHEN patient_id % 2 = 0 THEN 'Yes' ELSE 'No'
   END AS has_insurance,
   CASE WHEN patient_id % 2 = 0 THEN 10 ELSE 50
   END AS admission_cost
   FROM admissions
)
GROUP BY has_insurance
```

  </p>
</details>

###### 6. Show the provinces that has more patients identified as 'M' than 'F'. Must only show full province_name

<details>
  <summary>Solution</summary>
  <p>

```sql
SELECT province_name FROM patients
INNER JOIN province_names
USING(province_id)
GROUP BY province_name
HAVING SUM(gender = 'M') > SUM(gender ='F')
```

  </p>
</details>

###### 7. We are looking for a specific patient. Pull all columns for the patient who matches the following criteria:

- First_name contains an 'r' after the first two letters.
- Identifies their gender as 'F'
- Born in February, May, or December
- Their weight would be between 60kg and 80kg
- Their patient_id is an odd number
- They are from the city 'Kingston'

<details>
  <summary>Solution</summary>
  <p>

```sql
SELECT * FROM patients
WHERE first_name LIKE '__r%'
AND gender = 'F'
AND MONTH(birth_date) IN (2,5,12)
AND weight BETWEEN 60 AND 80
AND patient_id % 2 != 0
AND city = 'Kingston'
```

  </p>
</details>

###### 8. Show the percent of patients that have 'M' as their gender. Round the answer to the nearest hundreth number and in percent form.

<details>
  <summary>Solution</summary>
  <p>

```sql
SELECT CONCAT(ROUND(
  COUNT(CASE WHEN gender = 'M' THEN 1 END) * 100.0
  /
  COUNT(*)
  ,2),'%') AS percent_of_male
FROM patients
----
SELECT CONCAT(
  ROUND(
    AVG(CASE WHEN gender = 'M' THEN 1 ELSE 0 END) * 100.0
  ,2),'%') AS percent_of_male
FROM patients
```

  </p>
</details>
