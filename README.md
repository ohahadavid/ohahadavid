trading robot
def rsi(close_prices, window):

    """

    Calculates the Relative Strength Index (RSI) for a given window size.

    Args:

    close_prices (list): A list of closing prices.

    window (int): The number of periods to use in the RSI calculation.

    Returns:

    list: A list of RSI values.

    """

    deltas = np.diff(close_prices)

    seed = deltas[:window+1]

    up = seed[seed>=0].sum()/window

    down = -seed[seed<0].sum()/window

    rs = up/down

    rsi_values = [100 - (100 / (1 + rs))]

    for i in range(window, len(close_prices)):

        delta = deltas[i-1] # get the previous price change

        if delta > 0:

            upval = delta

            downval = 0

        else:

            upval = 0

            downval = -delta

        up = (up*(window-1) + upval) / window

        down = (down*(window-1) + downval) / window

        rs = up/down

        rsi_values.append(100 - (100 / (1 + rs)))

    return rsi_values

