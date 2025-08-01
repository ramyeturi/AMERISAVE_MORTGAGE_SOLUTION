I implemented a rule-based ranking model, focused on historical booking data and built entirely in SQL for real-time deployment. The ranking logic is simple yet robust, leveraging business-driven heuristics over statistical modeling.

The model evaluates agents across three core dimensions:
1. Relevant Booking Experience
Agents who have completed bookings to the same destination and from the same launch location are prioritized, as they have direct experience with the customer’s requested journey. This forms the primary ranking factor.
2. Customer Satisfaction Rating
To ensure quality of service, I incorporated the agent’s average customer service rating as a secondary sort key. This helps elevate agents who consistently provide exceptional customer experiences.
3. Years of Service
As a tertiary factor, I considered each agent’s tenure at the company. Longer tenure often reflects greater familiarity with internal processes, destinations, and customer expectations.

The model starts by filtering bookings that match the customer’s Destination and LaunchLocation.
I joined the space_travel_agents, assignment_history, and bookings tables to calculate:
•    The count of relevant completed bookings
•    The agent’s average rating
•    Their years of service
The final agent list is ordered descending by:
1)    RelevantBookingCount
2)    AverageCustomerServiceRating
3)    YearsOfService
This produces a stack-ranked list of agents best suited to handle the new lead.

