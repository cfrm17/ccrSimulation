# Counterparty Credit Risk Monte Carlo Simulation Methodology

Counterparty credit risk (CCR) is the risk of loss that will be incurred in the event of default by a counterparty. It will be incurred in the event of default by a counterparty. Only over-the-counter (OTC) derivatives and financial security transactions (e.g., repo) are subject to counterparty risk. If one party of a contract defaults, the non-defaulting party will find a similar contract with another counterparty in the market to replace the default one. That is why counterparty credit risk sometimes is referred as replacement risk. The replacement risk is the MTM value of a counterparty portfolio at the time of the counterparty default.

Counterparty credit risk measure is credit exposure. As credit exposures in future are stochastic, one needs to simulate market evolution in order to quantify CCR. This presentation provides some details about CCR simulation.

Keywords:
Counterparty credit risk, CCR, credit exposure, simulation model, calibration, stochastic process.


	Counterparty Credit Risk Definition
	Counterparty credit risk refers to the risk that a counterparty to a bilateral financial derivative contract may fail to fulfill its contractual obligation causing financial loss to the non-defaulting party.
	The risk that a counterparty defaults prior to expiration of a contract.
	If one party of a contract defaults, the non-defaulting party will find a similar contract with another counterparty in the market to replace the default one. That is why counterparty credit risk sometimes is referred as replacement risk.
	The replacement risk is the MTM value of a counterparty portfolio at the time of the counterparty default.
	Credit exposure (CE): the cost of replacing or hedging a contract at the time of default.
	Credit exposure is uncertain (stochastic) so that Monte Carlo simulation is needed

	Monte Carlo Simulation
	To calculate credit exposure or replacement cost in future times, one needs to simulate market evolutions. 
	Simulation must be conducted under the real-world measure.
	Simple solution
	Some vendors and institutions use this simplified approach
	Only a couple of stochastic processes are used to simulate all market risk factors.
	Use Vasicek model for all mean reverting factors
dr=k(θ-r)dt+σdW
where r – risk factor; k – drift; θ – mean reverse; σ – volatility; W – Wiener process
	Use Geometric Brownian Motion (GBM) for all non-mean reverting risk factors.
dS=μSdt+σSdW
	The calibration results for different risk factors are different from each other.
	Complex solution
	Different stochastic processes are used for different risk factors.
	Different calibration processes apply.
	Discuss this approach in details below

	Interest rate curve simulation
	Simulate yield curve or zero curve represented by yield rates or zero rates rather than swap curve represented by futures and swap rates.
	There are many points in a yield curve, e.g., 1d, 1w, 2w 1m, etc. One can use Principal Component Analysis (PCA) to convert, say, 20 points into 3 point drivers.
	Using PCA, you only need to simulate 3 drivers for each curve. But please remember you need to convert 3 drivers back to 20-point curve at each path and each time step.
	One popular IR simulation model under real-world measure is Cox-Ingersoll-Ross (CIR) model
dr=k(θ-r)dt+σ√r dW
 
	Reasons for choosing CIR model
	Positive interest rates
	Mean reversion process: empirically interest rates display a mean reversion behavior.
	Standard derivation in short term is proportional to the rate change.

	FX rate simulation
	Simulate spot foreign exchange rate.
	Black Karasinski (BK) model
d(ln⁡(r) )=k(ln⁡(θ)-ln⁡(r))dt+σdW
 

	Reasons for choosing BK model
	Lognormal distribution
	Non-negative FX rates
	Mean reversion process

	Equity price simulation
	Simulate spot stock price.
	Geometric Brownian Motion (GBM)
 
	Pros
	Simple
	Non-negative stock price
	Cons
	Simulated values could be extremely large for a longer horizon, so it may be better to incorporate with a reverting draft.

	Commodity simulation
	Simulate commodity spot, future and forward prices as well as pipeline spreads
	Simulate commodity implied volatilities
	Two factor model
log⁡(S_t )=q_t+X_t+Y_t
〖dX〗_t=(α_1-γ_1 X_t )dt+σ_1 〖dW〗_t^1
〖dY〗_t=(α_2-γ_2 Y_t )dt+σ_2 〖dW〗_t^2
〖dW〗_t^1 〖dW〗_t^2=ρdt
where	S_t – spot price or spread or implied volatility
	S_t – deterministic function
X_t – short term deviation
Y_t – long term equilibrium level
	The model leads to a closed form solution of forward prices and thus forward term structure.

	Implied volatility simulation
	Simulate equity implied volatility and FX implied volatility.
	Empirically implied volatilities are more volatile than prices.
	Stochastic volatility model , such as Heston model
〖dS〗_t=μS_t dt+√(V_t ) S_t 〖dW〗_t^1
〖dV〗_t=κ(θ-V_t )dt+ξ√(V_t ) 〖dW〗_t^2
〖dW〗_t^1 〖dW〗_t^2=ρdt
Where S_t is the implied volatility and V_t is the instantaneous variance of the implied volatility
	Pros
	Simulated distribution has fat tail or large skew and kurtosis
	Cons
	Complex implementation
	Unstable calibration
	A simple alternative
 
References:

https://finpricing.com/lib/IrCurveIntroduction.html

https://bitbucket.org/cfrm17/ccrsimulation/downloads/ccrSimulation-2.pdf


