# Life Insurance Pricing Mini Study

## What this project is
This project is a simple Excel model for pricing a **10-year term life insurance policy**.

The model estimates the **net single premium**, which is the expected present value of the death benefit.

I built it as a compact life actuarial project to understand and demonstrate:
- mortality-driven pricing
- survival probabilities
- discounting
- how premiums change by age and interest rate

---

## Product and assumptions
This model uses the following assumptions:

- Product: **10-year level term life insurance**
- Face amount: **$100,000**
- Issue ages tested: **30, 40, 50, 60**
- Interest rates tested: **3%, 5%, 7%**
- Mortality source: **SOA Standard Ultimate Life Table (SULT)**

This is a **simplified educational pricing model**. It focuses only on the expected present value of death benefits and does not include:
- expenses
- profit loading
- lapses
- reserves
- select mortality

---

## What the workbook contains

### 1. Inputs tab
This tab stores the main assumptions:
- face amount
- term
- interest rate

It is the control panel for the model.

### 2. Mortality_Table tab
This tab contains:
- `Age`
- `qx` = probability of death within one year at age x
- `px = 1 - qx` = probability of surviving one year at age x

The table includes only the age range needed for the project.

### 3. Pricing tab
This is the core calculation tab.

It calculates the expected present value of the death benefit year by year for one selected issue age.

For each policy year, the model determines:
- the attained age
- the mortality rate at that age
- the probability of surviving to the start of that year
- the discount factor
- the present value contribution from death during that year

These yearly contributions are added together to get the final net single premium.

### 4. Summary tab
This tab shows the final premium results across issue ages and interest-rate scenarios.

It is mainly used to compare how premiums change when:
- issue age increases
- interest rate changes

---

## What the model is calculating
The model calculates the **net single premium (NSP)**:

`NSP = expected present value of future death benefit payments`

For a 10-year term life policy, the model adds up the present value of the death benefit payment in each possible year of death.

In actuarial notation:

`NSP = S × Σ [ v^(k+1) × kpx × q(x+k) ]`

where:
- `S` = face amount
- `v = 1 / (1 + i)` = discount factor
- `kpx` = probability of surviving k years after issue
- `q(x+k)` = probability of death during the next year at attained age x+k

---

## How to think about the calculation
The logic is:

For each year of the 10-year term:
1. survive to the start of that year
2. die during that year
3. receive the $100,000 death benefit
4. discount that expected payment back to time 0

Then add all 10 years together.

So each row in the Pricing tab represents:

`face amount × survival probability × mortality probability × discount factor`

That gives one year's expected present value contribution.

Then all rows are summed.

---

## How the Pricing tab works
For each policy year, the columns represent:

- **Policy Year**: 1 to 10
- **Attained Age**: issue age + policy year - 1
- **qx**: mortality rate for that attained age
- **px**: one-year survival probability
- **Survival to Start**: probability of surviving to the start of that policy year
- **Discount Factor**: present value factor for payment at the end of that year
- **EPV Contribution**: expected present value of death benefit for that year

The final premium is:

`sum of all EPV contributions`

---

## Why the premium changes

### 1. Premium increases with age
As issue age rises, mortality rates rise.

That means the expected death benefit becomes larger, so the premium increases.

### 2. Premium decreases when interest rate increases
A higher interest rate means future payments are discounted more heavily.

That lowers the present value of expected death benefit payments, so the premium decreases.

---

## What this project is meant to show
This is not meant to be a production pricing model.

It is meant to show that I understand the basic mechanics of life insurance pricing:
- mortality assumptions
- survival probabilities
- present value logic
- sensitivity to age and discount rate

It also shows that I can translate actuarial ideas into a transparent Excel model.

---

## Data source
Mortality assumptions were manually extracted from the **Society of Actuaries Standard Ultimate Life Table (SULT)** published in the FAM-L exam tables.

Only a limited age range was used because this is a small educational model.

---

## Interview notes to remember
If I need to explain this project in an interview, the main points are:

- This is a **10-year term life pricing model**
- It estimates the **net single premium**
- It uses **SOA mortality assumptions**
- The premium is the **expected present value of death benefits**
- Each year's contribution reflects:
  - survival to that year
  - death in that year
  - discounting back to time 0
- Premium rises with age because mortality rises
- Premium falls with higher interest rates because discounting is stronger

---

## Why I built it
I built this project as a small life actuarial portfolio sample and as a way to practice the core logic behind mortality-based pricing in Excel.
