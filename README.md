# Energy Customer Integration Standard

## Introduction

The Energy Customer Integration Standard (ECIS) is a security framework and a communication protocol that is agreed to by both energy producer and utility provider that allows for the secure transportation of data on the basis of a "shared customer" (Resource Owner -> RO).

### Problem

Currently, there is no standard way for energy producers and utility providers to securely exchange germain data about their shared customers. Integrations are being written ad-hoc on an individual producer to provider level, at great cost to both parties, and in ways that could be improved from a security stance.

### Glossary

`Energy Producer` An entity that produces energy that is fed into the "grid." This entity may sell energy to "Utility Providers" or "Shared Customers."

`Utility Provider` An entity that operates grid infrastructure, and is the primary energy delivery party for a the "Shared Customers" needs.

`Shared Customer` An individual or entity that is a customer of both the "Energy Producer" and the "Utility Provider."

`ECI Provider` The entity which maintains the data of the Resource Owner. Typically, the "Utility Provider."

`ECI Consumer` The entity which may be authoized to gather data from the ECI Provider about the Resource Owner.

`Resource Owner` The individual or entity that may authorize the ECI Consumer to gather data from the ECI Provider.

## Technical Components

### Secturity

#### OAuth2

The integration is based on the OAuth2 flow. The resource owner must grant priveleges to the ECI Consumer on the ECI Provider systems in order for any data to be exchanged. More specifically, the ECI Consumer's access will be goverened by OAuth2 scopes.

#### JWT

Authentication should be verified with the use of JWTs.

---

### Communication Protocol

#### Request/Response Cycle

**Authorization**

Describe basic OAuth2 flow here

**Authenitcation**

Describe basic OAuth2 flow here

**ECI Request Types**

`ECI Basic Request`

During the request, the JWT should include the following claims:

```
{
    "system_account_id": "0018-102",
    "eci_request_type": "basic"
}
```

The response should respond with the following data:

- system_account_id
- account_type
- rate_code
- next_read_date
- meter_number
- producer_projects
- system_invoice_ids

`ECI Invoice Request`

During the request, the JWT should include the following claims:

```
{
    "system_account_id": "0018-102",
    "eci_request_type": "invoice"
    "system_invoice_id": "09183eef267"
}
```

The response should respond with the following data:

- system_account_id
- system_invoice_id
- rate_code
- next_read_date
- meter_number
- invoice_date
- invoice_due_date
- invoice_total
- invoice_paid
- service_period_start
- serivce_period_end

`ECI Invoice Detail Request`

During the request, the JWT should include the following claims:

```
{
    "system_account_id": "0018-102",
    "eci_request_type": "invoice_detail"
    "system_invoice_id": "09183eef267"
}
```

The response should respond with the following data:

- system_account_id
- system_invoice_id
- rate_code
- next_read_date
- meter_number
- invoice_date
- invoice_due_date
- invoice_total
- invoice_paid
- service_period_start
- serivce_period_end
- delivery_unit
- service_unit
- energy_consumption_quantity
- energy_consumption_rate
- energy_consumption_total
- distribution_quantity
- distribution_rate
- distribution_total
- transmission_quantity
- transmission_rate
- transmission_total
- stranded_costs_quantity
- stranded_costs_rate
- stranded_costs_total
- conservation_quantity
- conservation_rate
- conservation_total
- credit_unit
- credit_rate
- credit_carryover
- credit_new
- credit_allocated
- credit_remaining_total

---

### ECIS Vocabulary

`system_account_id`: (string) Unique identifier for the RO's account on the "provider" system.

`account_type`: (string) ("electric", "gas").

`rate_code`: (string) The rate code defined by the provider at which the resource owner is charged.

`billing_period_start`: (ISO formatted date string) The resource owner's last billing period start date.

`billing_period_end`: (ISO formatted date string) The resource owner's last billing period end date.

`next_read_date`: (ISO formatted date string) The resource owner's next meter reading date.

`meter_number`: (string) The meter number of the account.

`producer_projects`: (array<string>) List of renewable energy projects the account is allocated credits from.

`system_invoice_ids`: (array<string>) List of invoice ids that are associate with the resource owner, ordered by date.

`system_invoice_id`: (string) Unique identifier of an invoice that is associated with the resource owner.

`invoice_date`: (ISO formatted date string) The date the resource owner was issued their latest bill.

`invoice_due_date`: (ISO formatted date string) The resource owner's current bill due date.

`invoice_total`: (number) The total charge in USD for the resource owner's current bill.

`invoice_paid`: (boolean) If the resources owner's current bill is outstanding.

`service_period_start`: (ISO formatted date string) The service period start for the resource owner's current bill.

`serivce_period_end`: (ISO formatted date string) The service period end for the resource owner's current bill.

`delivery_unit`

`service_unit`

`energy_consumption_quantity`: (number)

`energy_consumption_rate`: (number)

`energy_consumption_total`: (number)

`distribution_quantity`: (number)

`distribution_rate`: (number)

`distribution_total`: (number)

`transmission_quantity`: (number)

`transmission_rate`: (number)

`transmission_total`: (number)

`stranded_costs_quantity`: (number)

`stranded_costs_rate`: (number)

`stranded_costs_total`: (number)

`conservation_quantity`: (number)

`conservation_rate`: (number)

`conservation_total`: (number)

`credit_unit`

`credit_rate`

`credit_carryover_total`

`credit_new_total`

`credit_allocated_total`

`credit_remaining_total`


## Discussion

A Resource Owner should not be scoped to one account per Provider.
