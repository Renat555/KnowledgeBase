# Содержание
[Подключение](#Подключение)  
[Создание модели](#Создание)  
[Стандартный запрос](#Стандартный)  
[Условия select](#Условия)  
[Группировка, количество результатов](#Группировка)

# Подключение
```
const Sequelize = require("sequelize");

const sequelize = new Sequelize("db_name", "db_user", "password", {
  dialect: "postgres",
  host: "localhost",
  define: {
    freezeTableName: true //чтобы название таблицы было как у модели, не в множественном числе
  },
});
```
# Создание модели

const modelName = sequelize.define("tableName", 
	{
	  columnName: {
		type: Sequelize.STRING,
		allowNull: false,
		unique: true //если у столбца внешний ключ, значения должны быть                              //уникальны
	  },
	},
	{ timestamps: false }
);

modelName.hasMany(modelName, { sourceKey: "column", foreignKey: "column" });
modelName.belongsTo(modelName, { targetKey: 'column', foreignKey: 'column' });

# Стандартный запрос
```
Product.findAll({
	attributes: [Sequelize.fn('DISTINCT', Sequelize.col('table.column')) ,'column'], //attributes - какое нужно поле
	raw: true,             //без дополнительных данных
	where: {
		maker: 'B'
	},
	include: [{            //данные из зависимой таблицы
		model: Laptop,
		attributes: ['price'],
		required: true //чтобы вывелись только значения которые есть в Laptop,
                               //cross-join, без этого будет left-join
	}],
}).then(users=>{
  console.log(users);
})

sequelize.literal(`(SELECT MAX(price) FROM printer)`) //можно вставить в attributes или where
```
# Условия select
```
Post.findAll({
  where: {
    [Op.and]: [{ a: 5 }, { b: 6 }],            // (a = 5) AND (b = 6)
    [Op.or]: [{ a: 5 }, { b: 6 }],             // (a = 5) OR (b = 6)
    someAttribute: {
      // Basics
      [Op.eq]: 3,                              // = 3
      [Op.ne]: 20,                             // != 20
      [Op.is]: null,                           // IS NULL
      [Op.not]: true,                          // IS NOT TRUE
      [Op.or]: [5, 6],                         // (someAttribute = 5) OR (someAttribute = 6)

      // Using dialect specific column identifiers (PG in the following example):
      [Op.col]: 'user.organization_id',        // = "user"."organization_id"

      // Number comparisons
      [Op.gt]: 6,                              // > 6
      [Op.gte]: 6,                             // >= 6
      [Op.lt]: 10,                             // < 10
      [Op.lte]: 10,                            // <= 10
      [Op.between]: [6, 10],                   // BETWEEN 6 AND 10
      [Op.notBetween]: [11, 15],               // NOT BETWEEN 11 AND 15

      // Other operators

      [Op.all]: sequelize.literal('SELECT 1'), // > ALL (SELECT 1)

      [Op.in]: [1, 2],                         // IN [1, 2]
      [Op.notIn]: [1, 2],                      // NOT IN [1, 2]

      [Op.like]: '%hat',                       // LIKE '%hat'
      [Op.notLike]: '%hat',                    // NOT LIKE '%hat'
      [Op.startsWith]: 'hat',                  // LIKE 'hat%'
      [Op.endsWith]: 'hat',                    // LIKE '%hat'
      [Op.substring]: 'hat',                   // LIKE '%hat%'
      [Op.iLike]: '%hat',                      // ILIKE '%hat' (case insensitive) (PG only)
      [Op.notILike]: '%hat',                   // NOT ILIKE '%hat'  (PG only)
      [Op.regexp]: '^[h|a|t]',                 // REGEXP/~ '^[h|a|t]' (MySQL/PG only)
      [Op.notRegexp]: '^[h|a|t]',              // NOT REGEXP/!~ '^[h|a|t]' (MySQL/PG only)
      [Op.iRegexp]: '^[h|a|t]',                // ~* '^[h|a|t]' (PG only)
      [Op.notIRegexp]: '^[h|a|t]',             // !~* '^[h|a|t]' (PG only)

      [Op.any]: [2, 3],                        // ANY (ARRAY[2, 3]::INTEGER[]) (PG only)
      [Op.match]: Sequelize.fn('to_tsquery', 'fat & rat') // match text search for strings 'fat' and 'rat' (PG only)

      // In Postgres, Op.like/Op.iLike/Op.notLike can be combined to Op.any:
      [Op.like]: { [Op.any]: ['cat', 'hat'] }  // LIKE ANY (ARRAY['cat', 'hat'])

    }
  }
});
```
# Группировка, количество результатов

Project.findAll({ group: 'name' }); // yields 'GROUP BY name'

Project.findAll({ limit: 10 }); // Fetch 10 instances/rows

Project.findAll({ offset: 8 }); // Skip 8 instances/rows

Project.findAll({ offset: 5, limit: 5 }); // Skip 5 instances and fetch the 5 after that
```
