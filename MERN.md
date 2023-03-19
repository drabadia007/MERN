# MERN

## code to connect to the mongo db database
module.exports = () => {
  const connectionParams = {
    useNewUrlParser: true,
    useUnifiedTopology: true,
  };

  try {
    mongoose.connect(process.env.MONGO_URL, connectionParams);
    console.log("connected to DB successfully");
  } catch (error) {
    console.log(error);
    console.log("error occured while connecting to the DB");
  }
};

## code to generate token by creating a funtion in Schema
UserSchema.methods.generateAuthtoken = async function () {
  try {
    let token23 = jwt.sign({ _id: this._id }, process.env.SECRET, {
      expiresIn: "1d",
    });

    this.tokens = this.tokens.concat({ token: token23 });
    await this.save();
    return token23;
  } catch (error) {
    res.status(422).json(error);
  }
};

## code for sample Schema
const UserSchema = new mongoose.Schema({
  fname: {
    type: String,
    requireed: true,
    trim: true,
  },
  email: {
    type: String,
    required: true,
    unique: true,
    validate(value) {
      if (!validator.isEmail(value)) {
        throw new Error("not a valid email");
      }
    },
  },
  password: {
    type: String,
    required: true,
    minLength: 6,
  },
  cpassword: {
    type: String,
    required: true,
    minLength: 6,
  },
  tokens: [
    {
      token: {
        type: String,
        required: true,
      },
    },
  ],
});




