# Life Insurance Pricing Mini Study

## What this project is

This project is a simple Excel model that estimates the **net single premium** for a **10-year term life insurance policy with a level $100,000 death benefit**.

The net single premium is the expected present value of the future death benefit under the model's mortality and interest-rate assumptions.

I built the project to understand and demonstrate:

- mortality-driven pricing mechanics
- conditional survival and death probabilities
- probability-weighted cash flows
- present-value discounting
- sensitivity to issue age and interest rate
- transparent Excel model structure and validation

---

## Product and assumptions

The model uses the following assumptions:

- Product: **10-year term life insurance with a level death benefit**
- Face amount: **$100,000**
- Benefit timing: **paid at the end of the policy year of death**
- Issue ages tested: **30, 40, 50, 60**
- Annual effective interest rates tested: **3%, 5%, 7%**
- Mortality source: **SOA Standard Ultimate Life Table (SULT)**

The interest-rate input is the annual effective rate `i`. The model converts that input into discount factors:

- `v = 1 / (1 + i)` is the one-year discount factor
- `v^t = (1 + i)^(-t)` is the discount factor for a payment at time `t`

This is a **simplified educational net-premium model**. It focuses on the expected present value of death benefits and does not include:

- expenses or commissions
- profit loading
- lapses
- reserves or capital requirements
- underwriting classes
- reinsurance
- select mortality
- annual premium-payment patterns
- company-specific product features or assumptions

---

## What the workbook contains

### 1. Inputs tab

This tab stores the main assumptions:

- face amount
- policy term
- annual effective interest rate `i`

It acts as the control panel for the model.

### 2. Mortality_Table tab

This tab contains:

- `Age`
- `qx` = probability of death within one year at age `x`, conditional on being alive at age `x`
- `px = 1 - qx` = probability of surviving one year at age `x`

The table includes only the age range required for the project.

### 3. Pricing tab

This is the core calculation tab.

It calculates the expected present value of the death benefit year by year for one selected issue age.

For each policy year, the model determines:

- attained age
- mortality rate at that age
- one-year survival probability
- probability of surviving to the start of the policy year
- time-specific discount factor `v^t`
- expected present value contribution from death during that year

The yearly contributions are added together to calculate the net single premium.

### 4. Summary tab

This tab presents the modeled net single premiums across issue ages and interest-rate scenarios.

It is used to compare how the result changes when:

- issue age increases
- the annual effective interest rate changes

---

## What the model is calculating

The model calculates the **net single premium (NSP)**:

`NSP = expected present value of future death benefit payments`

For a 10-year term life policy, the model sums the expected present value of the death benefit in each possible policy year of death.

In actuarial notation:

`NSP = S × Σ [ v^(k+1) × _k p_x × q_(x+k) ]`

where:

- `S` = face amount
- `i` = annual effective interest rate
- `v = 1 / (1 + i)` = one-year discount factor
- `v^(k+1)` = discount factor for a benefit paid at the end of policy year `k+1`
- `_k p_x` = probability of surviving `k` years after issue
- `q_(x+k)` = probability of death during the next year at attained age `x+k`, conditional on being alive at that age

---

## How to think about the calculation

For each year of the 10-year term, the model calculates the probability that the insured:

1. survives to the start of that policy year
2. dies during that policy year
3. receives the $100,000 death benefit at the end of that year

The expected payment is then discounted back to time 0.

Each row in the Pricing tab therefore represents:

`face amount × survival-to-start probability × conditional mortality rate × discount factor`

This gives one year's expected present value contribution. The ten annual contributions are then summed.

Death in a later policy year requires survival through all earlier policy years. The policy-year death events are therefore mutually exclusive and are not modeled as independent.

---

## How the Pricing tab works

For each policy year, the columns represent:

- **Policy Year**: 1 to 10
- **Attained Age**: issue age + policy year - 1
- **qx**: conditional mortality rate for the attained age
- **px**: one-year survival probability
- **Survival to Start**: cumulative probability of being alive at the start of the policy year
- **Discount Factor**: `v^t = (1 + i)^(-t)` for payment at the end of that year
- **EPV Contribution**: expected present value of the death benefit for that year

The final modeled premium is:

`sum of all EPV contributions`

---

## Why the modeled premium changes

### 1. Premium increases with issue age

As issue age rises, mortality rates generally rise. This increases the probability that the death benefit will be paid during the 10-year term, increasing its expected present value and therefore the modeled net single premium.

### 2. Premium decreases when the interest rate increases

The model inputs an annual effective interest rate `i`. A higher `i` produces a lower one-year discount factor `v = 1 / (1 + i)` and therefore lower time-specific discount factors `v^t`.

Because the future $100,000 benefit is fixed, the higher interest rate discounts that future payment more heavily. Its present value falls, so the modeled net single premium decreases, all else equal.

---

## What this project is meant to show

This is not a production pricing model.

It is intended to demonstrate that I understand the core mortality and present-value mechanics underlying a simplified life insurance net-premium calculation:

- mortality assumptions
- conditional survival and death probabilities
- probability-weighted cash flows
- annual effective interest-rate assumptions
- discount factors and present value
- sensitivity testing
- directional validation
- transparent Excel model structure

It also demonstrates that I understand the model's limitations and can distinguish a simplified net-premium calculation from full production pricing.

---

## Data source

Mortality assumptions were manually extracted from the **Society of Actuaries Standard Ultimate Life Table (SULT)** published in the FAM-L exam tables.

Only a limited age range was used because this is a small educational model.
