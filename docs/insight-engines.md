# Insight Engines

INTROSPECT powers its personal intelligence through **six purpose-built analytical engines**. Each engine evaluates multi-stream inputs to detect behavioral cause-and-effect loops.

---

## Engine 1: Screen-Sleep Degradation Engine
- **Inputs**: Late-night screen time ($t_{\text{screen}} > 23:00$), Total sleep duration ($T_{\text{sleep}}$), Sleep onset latency ($L_{\text{onset}}$).
- **Logic**: Evaluates linear and rank correlation between evening blue-light exposure and restorative sleep loss:
  $$\Delta T_{\text{sleep}} = \alpha \cdot t_{\text{late\_screen}} + \epsilon$$
- **Trigger Condition**: When late-night screen time exceeds 45 minutes, sleep deficit is projected at $\ge 40\text{ mins}$.
- **Output Action**: Recommends moving device to charging dock 30 minutes before target bedtime.

---

## Engine 2: Exercise-Recovery Synergy Engine
- **Inputs**: Workout duration ($D_{\text{workout}}$), Exercise intensity (METs / Heart rate reserve), Deep sleep stages ($T_{\text{deep}}$).
- **Logic**: Measures the parasympathetic rebound induced by daytime exertion:
  $$\text{Synergy Factor} = \frac{T_{\text{deep (workout day)}} - \bar{T}_{\text{deep (rest day)}}}{\bar{T}_{\text{deep (rest day)}}} \times 100\%$$
- **Observed Prototype Finding**: Workout days demonstrate a **+34% increase in deep sleep duration** (98 mins vs 65 mins).
- **Output Action**: Recommends optimal workout windows (at least 3 hours before sleep to ensure core temperature drop).

---

## Engine 3: Next-Day Activity Drag Engine
- **Inputs**: Nighttime screen time ($t_{\text{night}}$), Next-day step total ($S_{d+1}$), Day-of-week baseline ($\bar{S}_{\text{dow}}$).
- **Logic**: Quantifies the carryover fatigue penalty of bedtime digital usage on daytime kinetic activity:
  $$\text{Drag} = S_{d+1} - \bar{S}_{\text{dow}}$$
- **Observed Prototype Finding**: For each hour on phone in bed, next-day movement drops by approximately **1,400 steps**.
- **Output Action**: Alerts user that reclaiming 45 mins of bedtime yields ~1,500 passive next-day steps without workout willpower.

---

## Engine 4: Circadian Digital Clustering Engine
- **Inputs**: Hourly app usage distribution ($H_0 \dots H_{23}$), App category tags (Social, Video, Productivity).
- **Logic**: Computes Gini coefficient of daily usage to identify high-density distraction clusters:
  $$G = \frac{\sum_{i=1}^n \sum_{j=1}^n |x_i - x_j|}{2n^2 \bar{x}}$$
- **Observed Prototype Finding**: 54% of daily screen time is concentrated between 8:00 PM and 11:00 PM.
- **Output Action**: Suggests automated app-specific time boundaries starting at 8:30 PM.

---

## Engine 5: Attention Fragmentation & Interruption Engine
- **Inputs**: Total daily pickups ($P_{\text{total}}$), Awaken hours ($T_{\text{awake}}$), Notification load ($N_{\text{total}}$).
- **Logic**: Calculates mean inter-pickup interval (IPI):
  $$\text{IPI} = \frac{T_{\text{awake}} \times 60}{P_{\text{total}}}$$
- **Observed Prototype Finding**: 72 pickups over 16.5 waking hours = 1 pickup every 13.7 minutes.
- **Output Action**: Recommends batch notification delivery modes to restore sustained focus blocks.

---

## Engine 6: Lifestyle Harmony Index (LHI) Engine
- **Inputs**: Sleep consistency score ($C_{\text{sleep}}$), Activity fulfillment ($A_{\text{step}}$), Digital friction index ($F_{\text{digital}}$).
- **Formula**:
  $$\text{LHI} = w_1 \left(\frac{T_{\text{sleep}}}{T_{\text{target}}}\right) + w_2 \left(\frac{S_{\text{actual}}}{S_{\text{goal}}}\right) - w_3 \left(\frac{t_{\text{screen}}}{t_{\text{budget}}}\right)$$
- **Range**: 0 to 100 scale (Demo Value: **74 / 100**).
- **Output Action**: Provides the "Your Day at a Glance" executive summary badge.

