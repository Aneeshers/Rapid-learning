# General Trends
- Only Q is better than OnlyQFreeze
- QWPlasticFreeze is better than Only Q

# q012w003
Greater alpha Q (0.12) than alpha w (0.03)
- OnlyQ better than QFreeze
- Only Q better than OnlyWFreeze
![[OnlyQPlastic_vs_OnlyWPlasticFreeze.png]]
- Only Q plastic has a better starting RPE than QWPlastic, so does QFreeze
- OnlyQPlasticFreeze is better than QWPlasticFreeze
- OnlyQ and OnlyW plastic converged at same trial, but OnlyQ had a better starting RPE
- OnlyW better than WFreeze
- QWPlastic had a better starting RPE than OnlyW
- QWFreeze better than OnlyW
- QFreeze better than WFreeze
- QWPlastic better than QWFreeze

**Trends: OnlyQPlastic slightly better than QWPlastic and much better than OnlyWPlastic. QWPlastic has same convergence rate as OnlyWPlastic, but a lower starting RPE. Freeze models show similar behaviors. Non-freeze models better than Freeze models.** **

This suggests that learning Q here is more important than learning W.
# q0012w0003
- Only Q better than OnlyWFreeze
![[OnlyQPlastic_vs_OnlyWPlasticFreeze 1.png]]
- QWPlastic better than QPlastic
- OnlyQ better than QWFreeze
- OnlyQPlasticFreeze is better than QWPlasticFreeze
- OnlyQ has better starting RPE than OnlyW
- OnlyW better than OnlyWFreeze
- QWplastic better than OnlyW
- OnlyWFreeze couldn't converge below RPE 1.5, same with QWFreeze
- QWPlastic better than OnlyQFreeze
- QWPlastic converged, QWFreeze couldn't converge below 1.5 RPE

**Trends: QWPlastic beats out OnlyQPlastic and OnlyWplastic. OnlyQPlastic beats out OnlyWPlastic in starting RPE, but not necessarily convergence. Freeze models show similar behaviors. Non-freeze models better than Freeze models.** 

This suggests that learning Q and W here is the best and fastest method, with slight emphasis on Q.
# q0003w0012
- OnlyQ better than QFreeze
- Only Q does not converge below 1 RPE
- QWPlastic converges, so it's better than Only Q
- Only Q and OnlyQFreeze better than QWFreeze
- Only W converges so its better than Only Q
- OnlyW and OnlyWFreeze have very similar results, but OnlyW is slightly better
- OnlyW and WFreeze better than QFreeze and QWFreeze, although the QW's have better starting RPE's
- QW much better than OnlyQFreeze
- QW much better than OnlyWFreeze
- QW much better than QW Freeze

**Trends: QWPlastic beats OnlyQPlastic and OnlyWPlastic, although OnlyQPlastic has a better starting RPE than OnlyWPlastic, OnlyWPlastic converges to a lower RPE much faster. **

This suggests that both Q and W are very necessary. 
# q003w012
- OnlyQ better than QFreeze
- OnlyQ much better than WFreeze
- Only Q and QW have similar results but Only Q better starting RPE
- Only Q better than QW Freeze
- Q freeze better than QW freeze
- Only Q and Only W converge similarly, but Only Q has much lower starting RPE (same with Q freeze compared to Only W)
- Only W and W Freeze have similar results
- QW plastic has better starting RPE than Only W but similar convergence
- Only W better than QW freeze
- Qfreeze much better starting RPE than Wfreeze, but Wfreeze converges slightly faster
- QWPlastic better than QFreeze, WFreeze, and QWFreeze.

**Trends: OnlyQPlastic wins over OnlyWPlastic and QWPlastic, same trends with Freeze models, but non Freeze models beat Freeze models**

This suggests that W here is not important at all.


**Notes: what should we consider the starting point to be (thin in terms of W being randomly initialized or identity matrix)?**
- If Z is sensory cortex then we assume that cues are neutral and distinct perceptually - could be that it is gated out
- We predicted W as a way to learn the Go or No Go rule


- Think about initialization (try different W settings)
- dynamic learning rates
