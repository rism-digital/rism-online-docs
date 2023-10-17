# RISM Online Reconciliation API

The RISM Online Reconciliation API is suitable for use with [OpenRefine](https://openrefine.org). With this
service you can align your own data with data from RISM, allowing for easier linking and inter-connection between
datasets.

The RISM Online Reconciliation API URL is `https://rism.online/reconciliation/reconcile`.

There are two possible ways you might try to align your data. The first is to align by **value**, where you try to make the names or identifiers of things the same. If, for example, you want all people in your dataset to have the same form of name, including spelling, dates, and normalized "Lastname, Firstname".

Perhaps more useful, however, is to align by **identity**, where the goal is to add external identifiers for your own data to RISM. In this case, it means aligning the data so that you can say "person 123 in my dataset is the same as person 456 in RISM".

You can read more about how OpenRefine does reconciliation in the [OpenRefine documentation](https://openrefine.org/docs/manual/reconciling).

This service is still a work in progress. If you find problems, please let us know by [opening
an issue on GitHub](https://github.com/rism-digital/rism-online-issues/issues/).