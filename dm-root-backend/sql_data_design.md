Note: use UUID only

users
────────────────────────────────
id
email
phone (optional)
password_hash
role --enum platform_admin(me), customer
status -- UserStatus enum status can handle states such as active, suspended, inactive
email_verified
created_at
updated_at
last_login_at
deleted_at


refresh_tokens
────────────────────────────────
id
user_id
token_hash
expires_at
revoked_at
created_at


subscription_plans
────────────────────────────
id
code
name
description
is_active
sort_order
created_at
updated_at

subscription_plan_prices
────────────────────────────────────────

id                  UUID PK

plan_id             UUID FK → subscription_plans

currency            VARCHAR(3)
billing_interval    BillingInterval
amount              DECIMAL(12,2)

intro_amount        DECIMAL(12,2) NULL
intro_months        INT NULL

is_active           BOOLEAN

created_at          TIMESTAMP
updated_at          TIMESTAMP


subscriptions

This is the current subscription state of a user.

subscriptions
────────────────────────────────────────

id                      UUID PK

user_id                 UUID FK → users

plan_id                 UUID FK → subscription_plans
plan_price_id           UUID FK → subscription_plan_prices

status                  SubscriptionStatus

billing_interval        BillingInterval
currency                VARCHAR(3)
amount                  DECIMAL(12,2)

started_at              TIMESTAMP

current_period_start    TIMESTAMP
current_period_end      TIMESTAMP

cancel_at_period_end    BOOLEAN
cancelled_at            TIMESTAMP NULL
ended_at                TIMESTAMP NULL

created_at              TIMESTAMP
updated_at              TIMESTAMP


subscription_changes

This is the important addition for your upgrade/downgrade logic.

subscription_changes
────────────────────────────────────────

id                      UUID PK

subscription_id         UUID FK → subscriptions

change_type             SubscriptionChangeType

from_plan_id            UUID FK → subscription_plans NULL
from_plan_price_id      UUID FK → subscription_plan_prices NULL

to_plan_id              UUID FK → subscription_plans
to_plan_price_id        UUID FK → subscription_plan_prices

effective_at             TIMESTAMP

status                   SubscriptionChangeStatus

proration_amount        DECIMAL(12,2) NULL

created_at              TIMESTAMP
updated_at              TIMESTAMP


ENUM SubscriptionChangeType

UPGRADE
DOWNGRADE
CANCEL
REACTIVATE

And:

ENUM SubscriptionChangeStatus

PENDING
APPLIED
CANCELLED




