type Selectable interface {
	selectable()
}

type Querier[T any] interface {
	Get(ctx context.Context) (*T, error)
	GetMulti(ctx context.Context) ([]*T, error)
}

type Executor interface {
	Exec(ctx context.Context) (sql.Result, error)
}

type QueryBuilder interface {
	Build() (*Query, error)
}

type Expression interface {
	expr()
}

type Query struct {
	SQL  string
	Args []any
}

// Predicate 代表一个查询条件
// Predicate 可以通过和 Predicate 组合构成复杂的查询条件
type Predicate struct {
	left  Expression
	op    op
	right Expression
}